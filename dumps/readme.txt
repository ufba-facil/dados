     Intro:

Aqui estão descritos os passos executados para a criação do dump da base de dados que servirá para o projeto "UFBA Fácil*" (ver arquivo dump_meuhorario_mysql_XXXXXXXX.sql.gz nesta pasta). 
Para a criação desta base de dados são utilizados os modelos de entidades (que mapeiam as tabelas do banco) e os crawlers desenvolvidos no projeto do "MeuHorario 2".
Os crawlers são funções que desempenham o papel de popular a base de dados utilizando as entidades mapeadas e as informações obtidas nos sites da UFBA.



     O que é o UFBA Fácil*?

O UFBA Fácil* é um software para facilitar a solução de dependências de disciplinas para alunos da UFBA migrando de outros cursos. 
Inicialmente, ele está sendo desenvolvido para atender os cursos de Sistemas de Informação e Ciência da Computação.
O UFBA Fácil* ainda está em fase de desenvolvimento e será implementado utilizando tecnologias Web (PHP, HTML, CSS e JavaScript). 

* O nome "UFBA Fácil" é um nome temporário e não corresponde ao projeto final.



     O que é o MeuHorario 2?

MeuHorario 2 é um remake do simulador de matrícula MeuHorario e destina-se a ajudar os alunos da Universidade Federal da Bahia a planejar as aulas que participarão a cada semestre.
O MeuHorario original foi desenvolvido por Rodrigo Rocha em 2004 e pode ser acessado via o link http://meuhorario.dcc.ufba.br/.
O MeuHorario 2 utiliza o Ruby 2.3.1, Rails 5.0.0 e o PostgreSQL.



     Motivação:

Reaproveitar os modelos de entidade do MeuHorario 2; e reutilizar os algoritmos de geração de dados existentes (crawlers).
Facilitar a manutenção do banco de dados; e possibilitar a unificação das bases para sistemas distintos.



     Passo-a-passo:

Eis aqui o que você tem de fazer para popular a sua base MySQL:


1. Montar e configurar o ambiente Ruby on Rails no Linux/Mac:

Guia utilizado para configurar ambiente Ruby on Rails no Ubuntu: https://nandovieira.com.br/configurando-ruby-rails-mysql-postgresql-git-no-ubuntu

Dêem preferência a versão 2.3.1 do Ruby, pois é a versão utilizada na implementação do MeuHorario 2, assim como algumas das dependências do projeto requerem versão do Ruby inferior a 2.4.


2. Baixar o projeto do MeuHorario 2:

GitHub do MeuHorario 2: https://github.com/GabrielErbetta/meuhorario2


3. No arquivo Gemfile, onde tem escrito "gem 'pg'" mudar para "gem 'mysql2'" (ver arquivo Gemfile na pasta samples).

# Use MySQL as the database for Active Record
gem 'mysql2'


4. No arquivo config/database.yml, configurar o banco de dados MySQL que será utilizado para receber a carga de dados (ver arquivo database.yml na pasta samples).

development:
  adapter: mysql2
  host: <host>
  database: <database>
  pool: 5
  username: <username>
  password: <password>


5. Instalar as dependencias do projeto utilizando o comando:

bundle install


6. Migrar as tabelas da aplicação para a base configurada no passo 4, utilizando o comando:

rake db:migrate


7. Executar os crawlers para popular o banco de dados:

rake crawler:courses
rake crawler:disciplines
rake crawler:discipline_infos
rake crawler:pre_requisites
rake crawler:classes
rake crawler:areas

Obs.: Note que o crawler de areas não deve ser executado antes do crawler de courses, pois é ele quem "seta" o valor da coluna AREA_ID da tabela COURSES.

Pronto! Agora você já deve ter a sua base mapeada e populada.
