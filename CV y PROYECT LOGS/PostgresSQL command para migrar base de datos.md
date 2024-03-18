**hacer un dump**

```
pg_dump -h $POSTGRES_HOST -p $POSTGRES_PORT -U $POSTGRES_USER -f $FILE_NAME.sql $POSTGRES_DUMP_PARAMS $POSTGRES_DB

```

**restarura la base de datos ?**
```
pg_restore -h <hostname> -U <username> -d <db name> -Fd -j <NUM> -C <dump directory>

```

**restarura la base de datos**
```
psql -h $POSTGRES_HOST -p $POSTGRES_PORT -U $POSTGRES_USER -d $POSTGRES_DB < $FILE_NAME.sql  

```



**Conecta a la base de datos**
```
psql -Fd -d [nombre de la base de datps] -h [server name] -p [puerto] -U [nombre de usurio] 2> errors.log
```
- pide contraseña 
  


  


**Eliminando los datos actuales**

```
psql -h $POSTGRES_HOST -p $POSTGRES_PORT -U $POSTGRES_USER -d $POSTGRES_DB -c 'drop schema public cascade; create schema public;grant all on schema public to public;'

```

**Cargando nuevo archivo**

```
psql -h $POSTGRES_HOST -p $POSTGRES_PORT -U $POSTGRES_USER -d $POSTGRES_DB <$FILE_NAME.sql

```

**meow**

```

```
