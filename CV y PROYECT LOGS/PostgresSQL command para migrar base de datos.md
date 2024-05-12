**hacer un dump**

```
pg_dump -h $POSTGRES_HOST -p $POSTGRES_PORT -U $POSTGRES_USER -f $FILE_NAME.sql $POSTGRES_DUMP_PARAMS $POSTGRES_DB

```

**restaura la base de datos ?**
```
pg_restore -h <hostname> -U <username> -d <db name> -Fd -j <NUM> -C <dump directory>

```

importa la base de datos** (metodo probado)
```
psql -h $POSTGRES_HOST -p $POSTGRES_PORT -U $POSTGRES_USER -d $POSTGRES_DB < $FILE_NAME.sql  

```
psql -h kilimo-prod-mmrv-backend-db-azure.postgres.database.azure.com -U adminTerraform -p 5432 -d mmrvbackend > mmrv-backend-stg-2.sql


**Conecta a la base de datos**
```
psql -Fd -d [nombre de la base de datps] -h [server name] -p [puerto] -U [nombre de usurio] 2> errors.log
```
- pide contraseña 
psql -Fd -d mmrvbackend -h kilimo-prod-mmrv-backend-db-azure.postgres.database.azure.com -p 5432 -U adminTerraform  2> errors.log
  psql -h kilimo-prod-mmrv-backend-db-azure.postgres.database.azure.com -p 5432 -U adminTerraform -d mmrvbackend -c 'drop schema public cascade; create schema public;grant all on schema public to public;'

psql -h kilimo-prod-mmrv-backend-db-azure.postgres.database.azure.com -p 5432  -U adminTerraform -d mmrvbackend < mmrvbackend_dump.sql

psql -f mmrvbackend_dump.sql mmrvbackend -h kilimo-prod-mmrv-backend-db-azure.postgres.database.azure.com -p 5432 -U adminTerraform 2> errors.log

psql -h kilimo-prod-mmrv-backend-db-azure.postgres.database.azure.com -p 5432 -U adminTerraform -d mmrvbackend  -c 'drop schema public cascade; create schema public;grant all on schema public to public;'


**Eliminando los datos actuales**

```
psql -h $POSTGRES_HOST -p $POSTGRES_PORT -U $POSTGRES_USER -d $POSTGRES_DB -c 'drop schema public cascade; create schema public;grant all on schema public to public;'

```

**Cargando nuevo archivo**

```
psql -h $POSTGRES_HOST -p $POSTGRES_PORT -U $POSTGRES_USER -d $POSTGRES_DB <$FILE_NAME.sql

```


