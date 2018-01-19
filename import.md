### Como importar o dump através do comando mysql

## Importando / exportando um banco de dados MySQL com linhas de comando:

Para exportar um banco de dados MySQL (como um dump) através da linha de comando, execute:

```bash
mysqldump database_name > database_exportname.sql
```

Para importar um dump do MySQL em um banco de dados:

```bash
mysql database_name < database_exportname.sql
```

Para exportar todos os bancos de dados em um dump:

```bash
mysqldump --all-databases > all_databases_export.sql
```

Para importar um desses banco de dados MySQL do dump em um banco de dados:

```bash
mysql --one-database database_name < all_databases_export.sql
```

Traduzido do <https://coolestguidesontheplanet.com/import-export-mysql-database-command-line/>