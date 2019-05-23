# PostgreSQL CheatSheet

## Installation

## Ubuntu via snap
```
sudo snap install postgresql10
```
Note: if you install postgres using snap, you'll have to run PostgreSQL
commands such as `psql`, `pg_ctl`, `postgres`, etc. via wrappers that start
with a snap package name as prefix. For example, to run `pg_dump` you would run
`postgresql10.pgdump`, to run `dropdb` you would run `postgresql10.dropdb` and
so on.

Read more: https://github.com/commandprompt/postgresql-snap#running-commands

initialize cluster (you only need to run this once):
```
postgresql10.initialize initdb
```

start PostgreSQL:
```
postgresql10.pgctl -D ~/snap/postgresql10/common/data -l ~/snap/postgresql10/common/logs/logfile start
```

stop PostgreSQL:
```
postgresql10.pgctl -D ~/snap/postgresql10/common/data -l ~/snap/postgresql10/common/logs/logfile stop
```

## PSQL

connecting to postgres using psql:

In order to connect to a database you need to know the name of your target database, the host name and port number of the server, and what user name you want to connect as. psql can be told about those parameters via command line options, namely -d, -h, -p, and -U respectively.

When the defaults aren't quite right, you can save yourself some typing by setting the environment variables `PGDATABASE`, `PGHOST`, `PGPORT` and/or `PGUSER` to appropriate values.

An alternative way to specify connection parameters is in a conninfo string or a URI, which is used instead of a database name. 
For example:
```
psql postgresql://dbmaster:5433/mydb?sslmode=require
psql postgresql://user:secret@localhost/mydb
```

enter psql as postgres user:
```
sudo -u postgres psql
psql -U postgres
```

once you're in psql as the postgres user, you might want to create a role and 
database for your system user:
```
CREATE ROLE alexishevia LOGIN SUPERUSER;
CREATE DATABASE alexishevia OWNER=alexishevia;
```

now you should be able to connect to postgres with:
```
psql
```
(you will automatically be connected to your system user's database as your
system user)

toggle expanded display:
```
\x
```

quit psql:
```
\q
``` 

open current buffer using system editor:
```
\e
```

execute command from the current buffer:
```
\g
```

## Start / Restart Postgres

Ubuntu:
```
/etc/init.d/postgresql start
/etc/init.d/postgresql restart
```

## Configuration

show config file location:
```
SHOW config_file;
```

show data directory location:
```
SHOW data_directory;
```

show current settings:
```
SELECT * FROM pg_settings;
```

reload settings:
```
pg_ctl reload -D your_data_directory_here

sudo -u postgres /usr/lib/postgresql/9.1/bin/pg_ctl reload -D \
/var/lib/postgresql/9.1/main
```

## Databases

List databases
```
\l
```

Create database
```
# You can create a database from psql
CREATE DATABASE <nombre>;

# Or outside psql
createdb nombre
```

The owner of the database will be the logged in user and is a copy of `template1` database.

Switch to another database
```
\c DBNAME
```

Delete database
```
DROP DATABASE dbname
```

## Tablas

Show tables
```
\dt
```

Crear Tabla
```
CREATE TABLE <nombreTabla> (<campo1> <tipo de dato1>, <campo2> <tipo de dato2>, CONSTRAINT <nombre del constraint> PRIMARY KEY(<campo primario>));

CREATE TABLE "user" (userid SERIAL, username VARCHAR(15) UNIQUE NOT NULL, password VARCHAR(20) NOT NULL, CONSTRAINT usuariopkey PRIMARY KEY(userid));
```

Show tables on all schemas
```
\dt *.*
```

Show tables on specific schema
```
\dt schema_name.*
```

Describir Tabla
```
\d+ <nombre_tabla>
```

Eliminar tabla
```
DROP TABLE <nombre tabla>;
DROP TABLE "user";
```

Insertar Datos
```
INSERT INTO <nombreTabla> (<campo1>,<campo2>,<campoN>) VALUES (<valor1>,<valor2>,<valorN>);
INSERT INTO "user" (username, password) VALUES ('pepito', 'fd30!se?');
```

Borrar fila
```
DELETE FROM <nombreTabla> WHERE <campo>=<valor>;
DELETE FROM "user" WHERE userid=1;
```

## Data Types (Enums)

Show all data types:
```
\dT+
```


## Roles, Groups and Users

In PostgreSQL, there is really only one kind of an account and that is a role. Some roles can log in; when they have login rights, they are called users. Roles can be members of other roles, and when we have this kind of relationship, the containing roles are called groups.

`CREATE USER` is equivalent to `CREATE ROLE` except that `CREATE USER` automatically gives the `LOGIN` permission to the user/role. `CREATE ROLE` and `CREATE GROUP` are equivalent.

Ver usuarios existentes
```
\du
SELECT * FROM pg_shadow;
SELECT * FROM pg_user;
```

Crear usuario
```
CREATE ROLE <username> LOGIN PASSWORD '<password>' [CREATEDB | NOCREATEDB] [CREATEUSER | NOCREATEUSER] [SUPERUSER]

CREATE ROLE "testuser" LOGIN PASSWORD 'eg#r4_)ls1' CREATEDB NOCREATEUSER;
```

Eliminar usuario
```
DROP USER <username>
```

Crear grupo
```
CREATE ROLE <nombreGrupo> INHERIT;
```

Añadir usuario a un grupo
```
GRANT <nombreGrupo> TO <username>;
```

Eliminar usuario de un grupo
```
REVOKE <nombreGrupo> FROM <username>;
```

Ver grupos existentes
```
SELECT * FROM pg_group;
```

## Permisos
Darle permisos a un usuario
```
GRANT <permiso1>, <permisoN> ON <objectName> TO <username> 

GRANT ALL ON DATABASE mydb TO myusername;
```

Darle permisos a un grupo
```
GRANT <permiso1>, <permisoN> ON <objectName> TO GROUP <groupname> 
```

Los permisos pueden ser: SELECT, INSERT, UPDATE, DELETE, RULE, ALL
Los objetos pueden ser: tables, views, sequence

Remover permisos
```
REVOKE <permiso1>, <permisoN> ON <objectName> FROM <username> 
REVOKE <permiso1>, <permisoN> ON <objectName> FROM GROUP <groupname>
```

Ver permisos actuales
```
\z
```

## Schemas

A PostgreSQL database cluster contains one or more named databases. Users and groups of users are shared across the entire cluster, but no other data is shared across databases. Any given client connection to the server can access only the data in a single database, the one specified in the connection request.

A database contains one or more named _schemas_, which in turn contain tables. Schemas also contain other kinds of named objects, including data types, functions, and operators. The same object name can be used in different schemas without conflict; for example, both schema1 and myschema may contain tables named mytable. Unlike databases, schemas are not rigidly separated: a user may access objects in any of the schemas in the database he is connected to, if he has privileges to do so.

Create a schema
```
CREATE SCHEMA myschema;
```

Create a table inside a schema:
```
CREATE TABLE myschema.mytable (
 ...
);
```

To drop a schema including all contained objects
```
DROP SCHEMA myschema CASCADE;
```

Show schema search path
```
SHOW search_path;
```

List all schemas
```
\dn
```

## Extensions
List all installed extensions:
```
SELECT * FROM pg_available_extensions
WHERE comment LIKE '%string%' OR installed_version IS NOT NULL ORDER BY name; 
```

Install extension:
```
CREATE EXTENSION extension_name;

CREATE EXTENSION fuzzystrmatch;
```

Remove extension:
```
DROP EXTENSION extension_name;
```

## Import / Export
import sql file
```
\i filename.sql
\copy tablename FROM '/path/to/file.csv' DELIMITER ',' CSV
```

export data to a file
```
\copy (SELECT * FROM consumers LIMIT 100) TO 'consumers_export.csv' WITH CSV HEADER;
```

## Stored Procedures / Functions

show all user defined functions:
```
\df
```

show code for a stored procedure:
```
\df+ function\_name
```

## Random Numbers

The general rule to use rand to generate random numbers from {lower limit} to {upper limit} is:

select({upper limit - lower limit + 1} \* RANDOM() + {lower limit} )

So, to get numbers from 100000 to 999999: (all numbers in the 6-digit range)
```
select (900000 * RANDOM() + 100000)::int;
```

## Hashing Passwords
http://stackoverflow.com/questions/2647158/how-can-i-hash-passwords-in-postgresql

## Secure Signed Cookies
http://www.meetspaceapp.com/2016/04/19/cookie-signing-postgresql.html

## Geographical Distance
http://www.postgresql.org/docs/9.4/static/earthdistance.html

```
CREATE EXTENSION cube;
CREATE EXTENSION earthdistance;
```

get distance between two points
```
earth_distance(
  ll_to_earth(latitude1, longitude1),
  ll_to_earth(latitude2, longitude2)
) AS distance_in_meters;
```

find rows where distance is less than 100 meters from {50, -60}
```
SELECT *
FROM my_table
WHERE earth_box(ll_to_earth(50, -60), 100) @>
  ll_to_earth(my_table.latitude, my_table.longitude)
-- the @> operator sometimes includes points further than the specified
-- distance, so a second check using earth_distance is recommended
AND earth_distance(
  ll_to_earth(my_table.latitude, my_table.longitude),
  ll_to_earth(50, -60)
) < 100
```

create index for geographical search
```
CREATE INDEX location_index ON my_table 
USING gist (ll_to_earth((latitude)::double precision, (longitude)::double precision));
```

## UUIDs in Postgres
https://blog.starkandwayne.com/2015/05/23/uuid-primary-keys-in-postgresql

## Validations / Checks
[Porting ActiveRecord validations to Postgres](http://shuber.io/porting-activerecord-validations-to-postgres/)

## Indexes / Optimizations
[Check if your indexes are being used](https://www.compose.io/articles/simple-index-checking-for-postgres/)
[Agg: Parallel aggregations for PostgreSQL](http://firefoxoscentral.com/2015/12/firefox-os-is-dead-firefox-os-is-alive/)
[Streaming CSV from Postgres with ActionController::Live in Rails](https://lithostech.com/2015/08/streaming-csv-from-postgres-with-action-controller-live/)

## Autocomplete with Postgres
[Awesome Autocomplete: Trigram Search in Rails and PostgreSQL](https://www.sitepoint.com/awesome-autocomplete-trigram-search-in-rails-and-postgresql/)

## JSON
[Faster JSON Generation with PostgreSQL](https://hashrocket.com/blog/posts/faster-json-generation-with-postgresql)

## Full-Text Search
http://rachbelaid.com/postgres-full-text-search-is-good-enough
https://www.compose.com/articles/indexing-for-full-text-search-in-postgresql
https://about.gitlab.com/2016/03/18/fast-search-using-postgresql-trigram-indexes

- Búsqueda sencilla
 ```
  SELECT * FROM stops
  WHERE to_tsvector('spanish', description) @@ plainto_tsquery('spanish', 'hello world');
 ```

- Búsqueda utilizando operadores booleanos
  ```
  SELECT * FROM stops
  WHERE to_tsvector('spanish', description) @@ to_tsquery('spanish', 'par:*');

  SELECT * FROM stops
  WHERE to_tsvector('spanish', description) @@ to_tsquery('spanish', 'plaza & calle');

  SELECT * FROM stops
  WHERE to_tsvector('spanish', description) @@ to_tsquery('spanish', 'plaza | calle');
  ```

- Búsquedas en múltiples campos, asignando prioridad a cada campo.
  ```
     SELECT id,
            description,
            ts_rank(
              setweight(to_tsvector('spanish', name), 'A') ||
              setweight(to_tsvector('spanish', description), 'B'),
              to_tsquery('spanish', 'plaza | calle | hospital | avenida')
            ) AS rank
       FROM stops
   ORDER BY rank DESC
      LIMIT 10;
  ```
