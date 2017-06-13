
## <a name="add-a-database-to-the-availability-group"></a>Agregar una base de datos al grupo de disponibilidad

Asegúrese de la base de datos que se va a agregar al grupo de disponibilidad está en modo de recuperación completa y tiene una copia de seguridad de registro válido. Si se trata de una base de datos de prueba o una base de datos nueva, realice una copia de seguridad de base de datos. En el servidor principal de SQL, ejecute el siguiente Transact-SQL para crear y realizar copias de seguridad de una base de datos denominada `db1`.

```Transact-SQL
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'var/opt/mssql/data/db1.bak';
```

En la réplica principal de SQL Server, ejecute el siguiente Transact-SQL para agregar una base de datos denominada `db1` a un grupo de disponibilidad denominado `ag1`.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>Compruebe que la base de datos se crea en los servidores secundarios

En cada réplica secundaria de SQL Server, ejecute la siguiente consulta para ver si el `db1` base de datos se ha creado y está sincronizada.

```Transact-SQL
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
