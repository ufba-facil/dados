---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: default
---

<h3>Introdução:</h3>

Aqui estão descritos os passos executados para a criação do dump da base de dados que servirá para o projeto "UFBA Fácil" (ver arquivo [dump_meuhorario_mysql_20180116.sql.gz](https://ufbafacil.github.io/dados/dumps/dump_meuhorario_mysql_20180116.sql.gz)). 
<br/>Para a criação desta base de dados são utilizados os modelos de entidades (que mapeiam as tabelas do banco) e os crawlers desenvolvidos no projeto do "MeuHorario 2".
<br/>Os crawlers são funções que desempenham o papel de popular a base de dados utilizando as entidades mapeadas e as informações obtidas nos sites da UFBA.


<h3>O que é o UFBA Fácil?</h3>

O UFBA Fácil é um software para facilitar a solução de dependências de disciplinas para alunos da UFBA migrando de outros cursos. 
<br/>Inicialmente, ele está sendo desenvolvido para atender os cursos de Sistemas de Informação e Ciência da Computação.
<br/>O UFBA Fácil ainda está em fase de desenvolvimento e será implementado utilizando tecnologias Web (PHP, HTML, CSS e JavaScript). 

Obs.: O nome "UFBA Fácil" é um nome temporário e não corresponde ao projeto final.


<h3>O que é o MeuHorario 2?</h3>

O MeuHorario 2 é um remake do simulador de matrícula MeuHorario e destina-se a ajudar os alunos da Universidade Federal da Bahia a planejar as aulas que participarão a cada semestre.
<br/>O MeuHorario original foi desenvolvido por Rodrigo Rocha em 2004 e pode ser acessado via o link: http://meuhorario.dcc.ufba.br/.
<br/>O MeuHorario 2 utiliza o Ruby 2.3.1, Rails 5.0.0 e o PostgreSQL.


<h3>Motivação:</h3>

Reaproveitar os modelos de entidade do MeuHorario 2; e reutilizar os algoritmos de geração de dados existentes (crawlers).
<br/>Facilitar a manutenção do banco de dados; e possibilitar a unificação das bases para sistemas distintos.


<h3>Passo-a-passo:</h3>

Eis aqui o que você tem de fazer para popular a sua base MySQL:


**PASSO 1: Montar e configurar o ambiente Ruby on Rails no Linux/Mac:**

Guia utilizado para configurar ambiente Ruby on Rails no Ubuntu: https://nandovieira.com.br/configurando-ruby-rails-mysql-postgresql-git-no-ubuntu

Dêem preferência a versão 2.3.1 do Ruby, pois é a versão utilizada na implementação do MeuHorario 2, assim como algumas das dependências do projeto requerem versão do Ruby inferior a 2.4.


**PASSO 2: Baixar o projeto do MeuHorario 2:**

GitHub do MeuHorario 2: https://github.com/GabrielErbetta/meuhorario2


**PASSO 3: No arquivo Gemfile, onde tem escrito "gem 'pg'" mudar para "gem 'mysql2'" (ver arquivo Gemfile na pasta samples):**

_\# Use MySQL as the database for Active Record
<br/>gem 'mysql2'_


**PASSO 4: No arquivo config/database.yml, configurar o banco de dados MySQL que será utilizado para receber a carga de dados, conforme exemplo abaixo (ver arquivo database.yml na pasta samples):**

_development:<br/>
  adapter: mysql2<br/>
  host: \<my_host><br/>
  database: \<my_database><br/>
  pool: 5<br/>
  username: \<my_username><br/>
  password: \<my_password><br/>_


**PASSO 5: Instalar as dependencias do projeto utilizando o comando:**

_bundle install_


**PASSO 6: Migrar as tabelas da aplicação para a base configurada no passo 4, utilizando o comando:**

_rake db:migrate_


**PASSO 7: Executar os crawlers para popular o banco de dados:**

_rake crawler:courses<br/>
rake crawler:disciplines<br/>
rake crawler:discipline_infos<br/>
rake crawler:pre_requisites<br/>
rake crawler:classes<br/>
rake crawler:areas<br/>_

Obs.: Note que o crawler de areas não deve ser executado antes do crawler de courses, pois é ele quem "seta" o valor da coluna AREA_ID da tabela COURSES.

<h4>Pronto! Agora você já deve ter a sua base mapeada e populada.</h4>
