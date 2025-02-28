## *Identificació de la Versió de la Base de Dades*

Un atacant pot determinar la versió del motor de base de dades utilitzant consultes específiques segons el sistema:

### 🛢️ _Comandes per obtenir la versió_

|Base de Dades|Comanda per obtenir la versió|
|---|---|
|_MySQL_|SELECT @@version;|
|_PostgreSQL_|SELECT version();|
|_Oracle_|SELECT * FROM v$version;|
|_SQL Server_|SELECT @@version;|

---

## 📂 _Exploració de la Base de Dades_

Quan un atacant obté accés a la base de dades, pot llistar les bases de dades, taules i columnes disponibles.

### 📌 _Obtenir la base de dades actual_

|**Base de Dades**|**Comanda**|
|---|---|
|**MySQL**|`SELECT database();`|
|**PostgreSQL**|`SELECT current_database();`|
|**Oracle**|`SELECT name FROM v$database;`|
|**SQL Server**|`SELECT DB_NAME();`|

### 📌 _Llistar totes les bases de dades_

| **Base de Dades** | **Comanda**                                            |
| ----------------- | ------------------------------------------------------ |
| **MySQL**         | `SELECT schema_name FROM information_schema.schemata;` |
| **PostgreSQL**    | `SELECT datname FROM pg_database;`                     |
| **Oracle**        | `SELECT * FROM all_users;`                             |
| **SQL Server**    | `SELECT name FROM sys.databases;`                      |

### 📌 _Llistar taules en la base de dades actual_

| **Base de Dades** | **Comanda**                                                                         |
| ----------------- | ----------------------------------------------------------------------------------- |
| **MySQL**         | `SELECT table_name FROM information_schema.tables WHERE table_schema = database();` |
| **PostgreSQL**    | `SELECT tablename FROM pg_tables WHERE schemaname = 'public';`                      |
| **Oracle**        | `SELECT table_name FROM all_tables;`                                                |
| **SQL Server**    | `SELECT name FROM sys.tables;`                                                      |

### 📌 _Llistar columnes d'una taula específica

|**Base de Dades**|**Comanda**|
|---|---|
|**MySQL**|`SELECT column_name FROM information_schema.columns WHERE table_name = 'users';`|
|**PostgreSQL**|`SELECT column_name FROM information_schema.columns WHERE table_name = 'users';`|
|**Oracle**|`SELECT column_name FROM all_tab_columns WHERE table_name = 'USERS';`|
|**SQL Server**|`SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('users');`|

---

## 🔗 _Manipulació de dades amb funcions útils_

### 📌 _Concatenació de cadenes de text_

|Base de Dades|Funció de concatenació|
|---|---|
|_MySQL_|SELECT CONCAT(nom, ' ', cognom) FROM usuaris;|
|_PostgreSQL_|SELECT CONCAT(nom, ' ', cognom) FROM usuaris;|
|_Oracle_|SELECT nom|
|_SQL Server_|SELECT CONCAT(nom, ' ', cognom) FROM usuaris;|

- **Nota**: A _Oracle_, la concatenació es fa amb `||` en lloc de `CONCAT`.

### 📌 _Concatenació de valors de múltiples files en una sola cadena_

|Base de Dades|Funció per agrupar i concatenar|
|---|---|
|_MySQL_|SELECT GROUP_CONCAT(nom) FROM usuaris;|
|_PostgreSQL_|SELECT STRING_AGG(nom, ', ') FROM usuaris;|
|_Oracle_|SELECT LISTAGG(nom, ', ') WITHIN GROUP (ORDER BY nom) FROM usuaris;|
|_SQL Server_|SELECT STRING_AGG(nom, ', ') FROM usuaris;|

- **Explicació**:
    - `GROUP_CONCAT` (_MySQL_): Uneix els valors d'una columna en una sola cadena.
    - `STRING_AGG` (_PostgreSQL_ i _SQL Server_): Fa la mateixa funció que `GROUP_CONCAT`.
    - `LISTAGG` (_Oracle_): Funció equivalent que requereix `WITHIN GROUP`.

### 📌 _Obtenir el primer o últim valor d'un grup ordenat_

|Base de Dades|Funció per obtenir el primer/últim valor|
|---|---|
|_MySQL_|SELECT nom FROM usuaris ORDER BY data_creacio LIMIT 1;|
|_PostgreSQL_|SELECT nom FROM usuaris ORDER BY data_creacio LIMIT 1;|
|_Oracle_|SELECT nom FROM (SELECT nom FROM usuaris ORDER BY data_creacio) WHERE ROWNUM = 1;|
|_SQL Server_|SELECT TOP 1 nom FROM usuaris ORDER BY data_creacio;|

- En bases de dades modernes, també es pot usar `FIRST_VALUE(nom) OVER (ORDER BY data_creacio)`, si el sistema ho suporta.