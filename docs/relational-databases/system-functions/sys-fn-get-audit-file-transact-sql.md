---
title: Sys.fn_get_audit_file (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_get_audit_file_TSQL
- sys.fn_get_audit_file_TSQL
- fn_get_audit_file
- sys.fn_get_audit_file
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_get_audit_file function
- fn_get_audit_file function
ms.assetid: d6a78d14-bb1f-4987-b7b6-579ddd4167f5
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6dc30f57484714d70c7777a30ee43246c5980fcf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysfngetauditfile-transact-sql"></a>sys.fn_get_audit_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información de un archivo de auditoría creado por una auditoría de servidor en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_pattern*  
 Especifica el directorio o la ruta de acceso y el nombre de archivo del conjunto de archivos de auditoría que se van a leer. El tipo es **nvarchar (260)**. 
 
 - **SQL Server**:
    
    Este argumento debe incluir una ruta de acceso (letra de unidad o recurso compartido de red) y un nombre de archivo que pueda contener un carácter comodín. Un asterisco (*) sirve para recopilar varios archivos de un conjunto de archivos de auditoría. Por ejemplo:  
  
    -   **\<ruta de acceso >\\ \***  - recopila todos los archivos de auditoría de la ubicación especificada.  
  
    -   **\<ruta de acceso > \LoginsAudit_{GUID}** - recopila todos los archivos que tienen el nombre especificado y un par GUID de auditoría.  
  
    -   **\<ruta de acceso > \LoginsAudit_{GUID}_00_29384.sqlaudit** -recopilar un archivo de auditoría concreta.  
  
 - **Base de datos SQL Azure**:
 
    Este argumento se utiliza para especificar una dirección URL de blob (incluido el punto de conexión de almacenamiento y el contenedor). Mientras no se admite un carácter comodín asterisco, puede utilizar un prefijo de nombre de archivo parcial (blob) (en lugar del nombre del blob completo) para recopilar varios archivos (BLOB) que comienzan por este prefijo. Por ejemplo:
 
      - **\<Storage_endpoint\>/\<contenedor\>/\<ServerName\>/\<DatabaseName\> /**  -recopila todos los archivos de auditoría (BLOB) de la base de datos específica.    
      
      - **\<Storage_endpoint\>/\<contenedor\>/\<ServerName\>/\<DatabaseName\> / \< AuditName\>/\<CreationDate\>/\<FileName\>.xel** -recopila un archivo de auditoría concreta (blob).
  
> [!NOTE]  
>  Si se pasa una ruta de acceso sin un patrón de nombre de archivo, se producirá un error.  
  
 *initial_file_name*  
 Especifica la ruta y el nombre de un archivo específico del conjunto de archivos de auditoría desde el que hay que empezar a leer registros de auditoría. El tipo es **nvarchar (260)**.  
  
> [!NOTE]  
>  El *initial_file_name* argumento debe contener las entradas válidas o deben contener el predeterminado | Valor NULL.  
  
 *audit_record_offset*  
 Especifica una ubicación conocida con el archivo especificado para initial_file_name. Cuando se usa este argumento, la función inicia la lectura en el primer registro del búfer que está a continuación del desplazamiento especificado.  
  
> [!NOTE]  
>  El *audit_record_offset* argumento debe contener las entradas válidas o deben contener el predeterminado | Valor NULL. El tipo es **bigint**.  
  
## <a name="tables-returned"></a>Tablas devueltas  
 En la tabla siguiente se describe el contenido del archivo de auditoría que puede devolver esta función.  
  
|Nombre de columna|Tipo|Description|  
|-----------------|----------|-----------------|  
|event_time|**datetime2**|Fecha y hora cuando se desencadena la acción auditable. No admite valores NULL.|  
|sequence_number|**int**|Realiza un seguimiento de la secuencia de registros de un único registro de auditoría que era demasiado grande para caber en el búfer de escritura destinado a las auditorías. No admite valores NULL.|  
|action_id|**varchar(4)**|Id. de la acción. No admite valores NULL.|  
|succeeded|**bit**|Indica si la acción que desencadenó el evento se ha llevado a cabo correctamente. No admite valores NULL. Para todos los eventos que no sean los eventos de inicio de sesión, esto solo notifica si la comprobación del permiso tuvo o no tuvo éxito, no la operación.<br /> 1 = correcto<br /> 0 = error|  
|permission_bitmask|**varbinary (16)**|En algunas acciones, este es el permiso que se concedió, denegó o revocó.|  
|is_column_permission|**bit**|Marca que indica si éste es un permiso de nivel de columna. No admite valores NULL. Devuelve 0 si permission_bitmask = 0.<br /> 1 = verdadero<br /> 0 = falso|  
|session_id|**smallint**|Identificador de la sesión en la que se produjo el evento. No admite valores NULL.|  
|server_principal_id|**int**|Identificador del contexto de inicio de sesión en el que se realiza la acción. No admite valores NULL.|  
|database_principal_id|**int**|Identificador del contexto de usuario de la base de datos en el que se realiza la acción. No admite valores NULL. Devuelve 0 si esto no es aplicable. Por ejemplo, una operación de servidor.|  
|target_server_principal_id|**int**|Entidad de seguridad de servidor en la que se realiza la operación GRANT/DENY/REVOKE. No admite valores NULL. Devuelve 0 si no es aplicable.|  
|target_database_principal_id|**int**|Entidad de seguridad de base de datos en la que se realiza la operación GRANT/DENY/REVOKE. No admite valores NULL. Devuelve 0 si no es aplicable.|  
|object_id|**int**|Identificador de la entidad en la que se produjo la auditoría. Incluye lo siguiente:<br /> Objetos de servidor<br /> Bases de datos<br /> Objetos de base de datos<br /> Objetos de esquema<br /> No admite valores NULL. Devuelve 0 si la entidad es el propio servidor o si la auditoría no se realiza en un nivel de objeto. Por ejemplo, la autenticación.|  
|class_type|**varchar(2)**|El tipo de entidad auditable en la que se produce la auditoría. No admite valores NULL.|  
|session_server_principal_name|**sysname**|Entidad de seguridad de servidor para la sesión. Acepta valores NULL.|  
|server_principal_name|**sysname**|Inicio de sesión actual. Acepta valores NULL.|  
|server_principal_sid|**varbinary**|SID del inicio de sesión actual. Acepta valores NULL.|  
|database_principal_name|**sysname**|Usuario actual. Acepta valores NULL. Devuelve NULL si no está disponible.|  
|target_server_principal_name|**sysname**|Inicio de sesión de destino de acción. Acepta valores NULL. Devuelve NULL si no es aplicable.|  
|target_server_principal_sid|**varbinary**|SID del inicio de sesión de destino. Acepta valores NULL. Devuelve NULL si no es aplicable.|  
|target_database_principal_name|**sysname**|Usuario de destino de la acción. Acepta valores NULL. Devuelve NULL si no es aplicable.|  
|server_instance_name|**sysname**|Nombre de la instancia de servidor donde se ha producido la auditoría. Se usa el formato servidor\instancia estándar.|  
|database_name|**sysname**|Contexto de base de datos en el que se produjo la acción. Acepta valores NULL. Devuelve NULL para las auditorías que se realizan en el nivel de servidor.|  
|schema_name|**sysname**|El contexto del esquema en el que se produjo la acción. Acepta valores NULL. Devuelve NULL para las auditorías que se producen fuera de un esquema.|  
|object_name|**sysname**|El nombre de la entidad en la que se produjo la auditoría. Incluye lo siguiente:<br /> Objetos de servidor<br /> Bases de datos<br /> Objetos de base de datos<br /> Objetos de esquema<br /> Acepta valores NULL. Devuelve NULL si la entidad es el propio servidor o si la auditoría no se realiza en un nivel de objeto. Por ejemplo, la autenticación.|  
|instrucción|**nvarchar(4000)**|Instrucción TSQL, si existe. Acepta valores NULL. Devuelve NULL si no es aplicable.|  
|additional_information|**nvarchar(4000)**|La información única que se aplica exclusivamente a un evento se devuelve como XML. Este tipo de información está incluida en un pequeño número de acciones de auditoría.<br /><br /> Un nivel de pila de TSQL se mostrará en formato XML para las acciones que tienen asociada la pila de TSQL. El formato XML será:<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> Frame nest_level indica el nivel de anidamiento actual del marco. El nombre del módulo se representa en formato de tres partes (nombreDeBaseDeDatos, nombreDeEsquema y nombreDeObjeto).  El nombre del módulo se analizará para escape caracteres xml no válidos, como `'\<'`, `'>'`, `'/'`, `'_x'`. Se produce el escape como `_xHHHH\_`. HHHH representa el código UCS-2 hexadecimal de cuatro dígitos para el carácter.<br /><br /> Acepta valores NULL. Devuelve NULL si el evento no proporciona información adicional.|  
|file_name|**varchar(260)**|Ruta de acceso y nombre del archivo de registro de auditoría del que procede el registro. No admite valores NULL.|  
|audit_file_offset|**bigint**|Desplazamiento de búfer del archivo que contiene el registro de auditoría. No admite valores NULL.|  
|user_defined_event_id|**smallint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Id. de evento definido por usuario que se pasa como argumento a **sp_audit_write**. **NULL** para eventos del sistema (valor predeterminado) y distinto de cero para el evento definido por el usuario. Para obtener más información, consulte [sp_audit_write &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md).|  
|user_defined_information|**nvarchar(4000)**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Usa para registrar información adicional que el usuario desea grabar en |registro de auditoría mediante el uso de la **sp_audit_write** procedimiento almacenado.|  
|audit_schema_version |**int** | |  
|sequence_group_id |**varbinary** | **Se aplica a**: sólo servidor SQL Server (a partir de 2016) |  
|transaction_id |**bigint** | **Se aplica a**: sólo servidor SQL Server (a partir de 2016) |  
|client_ip |**nvarchar(128)** | **Se aplica a**: base de datos de SQL Azure + SQL Server (a partir de 2017) |  
|application_name |**nvarchar(128)** | **Se aplica a**: base de datos de SQL Azure + SQL Server (a partir de 2017) |  
|duration_milliseconds |**bigint** | **Se aplica a**: la base de datos de SQL Azure solo |  
|response_rows |**bigint** | **Se aplica a**: la base de datos de SQL Azure solo |  
|affected_rows |**bigint** | **Se aplica a**: la base de datos de SQL Azure solo |  
|connection_id |GUID | **Se aplica a**: la base de datos de SQL Azure solo |
|data_sensitivity_information |nvarchar(4000) | **Se aplica a**: la base de datos de SQL Azure solo |
  
## <a name="remarks"></a>Comentarios  
 Si el *file_pattern* argumento pasado a **fn_get_audit_file** hace referencia a una ruta de acceso o un archivo que no existe, o si el archivo no es un archivo de auditoría, el **MSG_INVALID_AUDIT_FILE**mensaje de error.  
  
## <a name="permissions"></a>Permissions  
 - **SQL Server**: requiere la **CONTROL SERVER** permiso.  
 - **La base de datos de SQL Azure**: requiere la **CONTROL DATABASE** permiso.     
    - Administradores de servidor pueden tener acceso a los registros de auditoría de todas las bases de datos en el servidor.
    - Administradores de servidor no solo pueden tener acceso a los registros de auditoría de la base de datos actual.
    - Se omitirán los blobs que no cumplen los criterios anteriores (una lista de blobs omitidos se mostrará en el mensaje de salida de consulta), y la función devolverá registros solo de blobs para el que se permite el acceso.  
  
## <a name="examples"></a>Ejemplos

- **SQL Server**

  En este ejemplo se lee un archivo denominado `\\serverName\Audit\HIPPA_AUDIT.sqlaudit`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPPA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Azure SQL Database**

  En este ejemplo se lee de un archivo denominado `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`:  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  Este ejemplo se lee desde el mismo archivo que anteriormente, pero con las cláusulas de T-SQL adicionales (**arriba**, **ORDER BY**, y **donde** cláusula para filtrar los registros de auditoría devueltos por el función):
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  Este ejemplo se leen todos los registros de los servidores que comienzan por de auditoría `Sh`: 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

Para ver un ejemplo completo de cómo crear una auditoría, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).

Para obtener información sobre la configuración de auditoría de base de datos de SQL Azure, consulte [Introducción a la auditoría de base de datos SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).
  
## <a name="see-also"></a>Vea también  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Crear una auditoría de servidor y una especificación de auditoría de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
