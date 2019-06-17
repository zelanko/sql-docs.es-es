---
title: Uso de SID de servicio para conceder permisos a servicios en SQL Server | Microsoft Docs
author: randomnote1
ms.author: dareist
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.openlocfilehash: 1a0bd129fc535b53d8d19ad76f99f3a86ba10c11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65135241"
---
# <a name="using-service-sids-to-grant-permissions-to-services-in-sql-server"></a>Uso de SID de servicio para conceder permisos a servicios en SQL Server

SQL Server usa [identificadores de seguridad (SID) por servicio](https://support.microsoft.com/help/2620201/sql-server-uses-a-service-sid-to-provide-service-isolation) para permitir la concesión de los permisos directamente a un servicio específico. Este método lo usa SQL Server para conceder permisos a los servicios de motor y agente (NT SERVICE\MSSQL$<InstanceName> y NT SERVICE\SQLAGENT$<InstanceName>, respectivamente). Con este método, estos servicios pueden acceder al motor de base de datos solo cuando se ejecutan los servicios.

Este mismo método se puede usar cuando se conceden permisos a otros servicios. El uso de un SID de servicio elimina la sobrecarga de administrar y mantener las cuentas de servicio y proporciona un control más granular y más preciso sobre los permisos concedidos a los recursos del sistema.

Ejemplos de servicios donde se puede usar un SID de servicio:

- Servicio de mantenimiento de System Center Operations Manager (NT SERVICE\HealthService)
- Servicio de Clústeres de conmutación por error de Windows Server (WSFC) (NT SERVICE\ClusSvc)

Algunos servicios no disponen de un SID de servicio de forma predeterminada. El SID de servicio debe crearse con [SC.exe](https://docs.microsoft.com/windows/desktop/services/configuring-a-service-using-sc). [Este método](https://kevinholman.com/2016/08/25/sql-mp-run-as-accounts-no-longer-required/) lo han adoptado los administradores de Microsoft System Center Operations Manager para conceder permiso para el Servicio de mantenimiento en SQL server.

Una vez se haya creado y confirmado el servicio de SID, se debe conceder permiso en SQL Server. La concesión de permisos se lleva a cabo mediante la creación de un inicio de sesión en Windows con [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) o una consulta. Una vez creado el inicio de sesión, se le pueden conceder permisos, agregar a roles y asignar a bases de datos al igual que cualquier otro inicio de sesión.

> [!TIP]
> Si se recibe el error `Login failed for user 'NT AUTHORITY\SYSTEM'`, compruebe que existe el SID de servicio para el servicio deseado, que el inicio de sesión de SID de servicio se ha creado en SQL Server y que se han concedido los permisos adecuados para el SID de servicio en SQL Server.

## <a name="security"></a>Seguridad

### <a name="eliminate-service-accounts"></a>Eliminación de cuentas de servicio

Tradicionalmente, las cuentas de servicio se han usado para permitir que los servicios inicien sesión en SQL Server. Las cuentas de servicio agregan una capa adicional de complejidad de administración ya que tienen que mantener y actualizar con frecuencia la contraseña de la cuenta de servicio. Además, las credenciales de la cuenta de servicio las podría usar una persona que intentara ocultar sus actividades cuando realizara acciones en la instancia.

### <a name="granular-permissions-to-system-accounts"></a>Permisos granulares a las cuentas del sistema

Las cuentas del sistema históricamente han concedido permisos mediante la creación de un inicio de sesión para las cuentas [LocalSystem](https://msdn.microsoft.com/library/windows/desktop/ms684190) ([NT AUTHORITY\SYSTEM en en-us](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions#Localized_service_names)) o [NetworkService](https://docs.microsoft.com/windows/desktop/Services/networkservice-account) ([ NT AUTHORITY\NETWORK SERVICE en en-us](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?#Localized_service_names)) y la concesión de esos permisos de los inicios de sesión. Este método concede cualquier permiso de proceso o servicio en SQL, que se ejecuta como una cuenta del sistema.

El uso de un SID de servicio permite que los permisos se concedan a un servicio específico. El servicio solo tiene acceso a los recursos cuyos permisos se le han concedido cuando se está ejecutando. Por ejemplo, si la `HealthService` se está ejecutando como `LocalSystem` y se le concede `View Server State`, la cuenta `LocalSystem` solo tendrá permiso para `View Server State` cuando se esté ejecutando en el contexto de la `HealthService`. Si cualquier otro proceso intenta acceder al estado del servidor de SQL como `LocalSystem`, se le denegará el acceso.

## <a name="examples"></a>Ejemplos

### <a name="a-create-a-service-sid"></a>A. Creación de un SID de servicio

El siguiente comando de PowerShell creará un SID de servicio en el servicio de mantenimiento de System Center Operations Manager.

```PowerShell
sc.exe --% sidtype "HealthService" unrestricted
```

> [!IMPORTANT]
> `--%` indica a PowerShell detener el análisis del resto del comando. Esto es útil cuando se usan comandos y aplicaciones heredados.

### <a name="b-query-a-service-sid"></a>B. Realización de una consulta de un SID de servicio

Para comprobar un SID de servicio o para garantizar que un SID de servicio existe, ejecute el siguiente comando en PowerShell.

```PowerShell
sc.exe --% qsidtype "HealthService"
```

> [!IMPORTANT]
> `--%` indica a PowerShell detener el análisis del resto del comando. Esto es útil cuando se usan comandos y aplicaciones heredados.

### <a name="c-add-a-newly-created-service-sid-as-a-login"></a>C. Adición de un SID de servicio recién creado como un inicio de sesión

El ejemplo siguiente crea un inicio de sesión para el servicio de mantenimiento de System Center Operations Manager con T-SQL.

```SQL
CREATE LOGIN [NT SERVICE\HealthService] FROM WINDOWS
GO
```

### <a name="d-add-an-existing-service-sid-as-a-login"></a>D. Adición de un SID de servicio existente como un inicio de sesión

El ejemplo siguiente crea un inicio de sesión para el servicio de clúster con T-SQL. La concesión directa de permisos al servicio de clúster elimina la necesidad de conceder permisos excesivos para la cuenta del SISTEMA.

```SQL
CREATE LOGIN [NT SERVICE\ClusSvc] FROM WINDOWS
GO
```

### <a name="e-grant-permissions-to-a-service-sid"></a>E. Concesión de permisos al SID de servicio

Conceda los permisos necesarios con el fin de administrar grupos de disponibilidad para el servicio de clúster.

```SQL
GRANT ALTER ANY AVAILABILITY GROUP TO 'NT SERVICE\ClusSvc'
GO

GRANT CONNECT SQL TO 'NT SERVICE\ClusSvc'
GO

GRANT VIEW SERVER STATE TO 'NT SERVICE\ClusSvc'
GO
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la estructura de SID de servicio, consulte [Estructura de SERVICE_SID_INFO](https://docs.microsoft.com/windows/desktop/api/winsvc/ns-winsvc-_service_sid_info).

Obtenga información sobre las opciones adicionales que están disponibles cuando se [crea un inicio de sesión](https://docs.microsoft.com/sql/t-sql/statements/create-login-transact-sql).

Para usar seguridad basada en roles con los SID de servicio, obtenga información sobre [crear roles](https://docs.microsoft.com/sql/t-sql/statements/create-role-transact-sql) en SQL Server.

Obtenga información sobre diferentes formas de [conceder permisos](https://docs.microsoft.com/sql/t-sql/statements/grant-transact-sql) a SID de servicio en SQL Server.
