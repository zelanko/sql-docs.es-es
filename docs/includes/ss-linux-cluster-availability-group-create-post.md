---
ms.openlocfilehash: 0cdc343bf4ea6866d1a55672187451a3b6d95ec1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68215568"
---

## <a name="add-a-database-to-the-availability-group"></a>Agregar una base de datos al grupo de disponibilidad

Asegúrese de que la base de datos que se agrega al grupo de disponibilidad está en modo de recuperación completa y tiene una copia de seguridad de registros válida. Si se trata de una base de datos de prueba o una base de datos recién creada, realice una copia de seguridad de base de datos. En el servidor de SQL Server principal, ejecute el script de Transact-SQL siguiente para crear una base de datos denominada `db1` y realizar una copia de seguridad de ella:

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

En la réplica principal de SQL Server, ejecute el script de Transact-SQL siguiente para agregar una base de datos denominada `db1` a un grupo de disponibilidad denominado `ag1`:

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>Compruebe que la base de datos se crea en los servidores secundarios.

En todas las réplicas secundarias de SQL Server, ejecute la consulta siguiente para ver si la base de datos `db1` se ha creado y está sincronizada:

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
