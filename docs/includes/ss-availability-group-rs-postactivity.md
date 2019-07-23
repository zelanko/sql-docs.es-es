---
ms.openlocfilehash: bf755ccfe5a1a6816129173dcb6ad5050ea5e114
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213323"
---

## <a name="add-a-database-to-the-availability-group"></a>Agregar una base de datos al grupo de disponibilidad

Asegúrese de que la base de datos que se agrega al grupo de disponibilidad está en modo de recuperación completa y tiene una copia de seguridad de registros válida. Si la base de datos es una base de datos de prueba o una base de datos recién creada, realice una copia de seguridad. Para crear una base de datos denominada `db1` y realizar una copia de seguridad de ella, ejecute el script de Transact-SQL siguiente en la instancia principal de SQL Server:

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1]
   TO DISK = N'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\db1.bak';
```

Para agregar una base de datos denominada `db1` a un grupo de disponibilidad denominado `ag1`, ejecute el script de Transact-SQL siguiente en la réplica principal de SQL Server:

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>Compruebe que la base de datos se crea en los servidores secundarios.

Para ver si la base de datos `db1` se ha creado y está sincronizada, ejecute la consulta siguiente en todas las réplicas secundarias de SQL Server:

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
