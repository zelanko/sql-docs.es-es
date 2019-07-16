---
title: sys.fn_get_audit_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 350b1eca94f8041a0a38105c650e1c0ec7e1f617
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046286"
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
 Especifica el directorio o la ruta de acceso y el nombre de archivo del conjunto de archivos de auditoría que se van a leer. El tipo es **nvarchar (260)** . 
 
 - **SQL Server**:
    
    Este argumento debe incluir una ruta de acceso (letra de unidad o recurso compartido de red) y un nombre de archivo que pueda contener un carácter comodín. Un asterisco (*) sirve para recopilar varios archivos de un conjunto de archivos de auditoría. Por ejemplo:  
  
    -   **\<ruta de acceso >\\ \***  : recopile todos los archivos de auditoría de la ubicación especificada.  
  
    -   **\<ruta de acceso > \LoginsAudit_{GUID}** : recopile todos los archivos que tienen el nombre especificado y un par GUID de auditoría.  
  
    -   **\<ruta de acceso > \LoginsAudit_{GUID}_00_29384.sqlaudit** -recopilar un archivo de auditoría concreta.  
  
 - **Azure SQL Database**:
 
    Este argumento se utiliza para especificar una dirección URL del blob (incluido el punto de conexión de almacenamiento y el contenedor). Aunque no se admite un carácter comodín asterisco, puede usar un prefijo de nombre de archivo parcial (blob) (en lugar del nombre del blob completo) para recopilar varios archivos (BLOB) que comienzan por este prefijo. Por ejemplo:
 
      - **\<Storage_endpoint\>/\<contenedor\>/\<ServerName\>/\<DatabaseName\> /**  -recopila todos los archivos de auditoría (BLOB) para la base de datos específica.    
      
      - **\<Storage_endpoint\>/\<contenedor\>/\<ServerName\>/\<DatabaseName\> / \< AuditName\>/\<CreationDate\>/\<FileName\>.xel** -recopila un archivo de auditoría específicos (blob).
  
> [!NOTE]  
>  Si se pasa una ruta de acceso sin un patrón de nombre de archivo, se producirá un error.  
  
 *initial_file_name*  
 Especifica la ruta y el nombre de un archivo específico del conjunto de archivos de auditoría desde el que hay que empezar a leer registros de auditoría. El tipo es **nvarchar (260)** .  
  
> [!NOTE]  
>  El *initial_file_name* argumento debe contener entradas válidas o debe contener el predeterminado | Valor NULL.  
  
 *audit_record_offset*  
 Especifica una ubicación conocida con el archivo especificado para initial_file_name. Cuando se usa este argumento, la función inicia la lectura en el primer registro del búfer que está a continuación del desplazamiento especificado.  
  
> [!NOTE]  
>  El *audit_record_offset* argumento debe contener entradas válidas o debe contener el predeterminado | Valor NULL. El tipo es **bigint**.  
  
## <a name="tables-returned"></a>Tablas devueltas  
 En la tabla siguiente se describe el contenido del archivo de auditoría que puede devolver esta función.  
  
| Nombre de columna | Type | Descripción |  
|-------------|------|-------------|  
| action_id | **varchar(4)** | Id. de la acción. No acepta valores NULL. |  
| additional_information | **nvarchar(4000)** | La información única que se aplica exclusivamente a un evento se devuelve como XML. Este tipo de información está incluida en un pequeño número de acciones de auditoría.<br /><br /> Un nivel de pila de TSQL se mostrará en formato XML para las acciones que tienen asociada la pila de TSQL. El formato XML será:<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> Frame nest_level indica el nivel de anidamiento actual del marco. El nombre del módulo se representa en formato de tres partes (nombreDeBaseDeDatos, nombreDeEsquema y nombreDeObjeto).  El nombre del módulo se analizará para escapar caracteres xml no válidos, como `'\<'`, `'>'`, `'/'`, `'_x'`. Se produce el escape como `_xHHHH\_`. HHHH representa el código UCS-2 hexadecimal de cuatro dígitos para el carácter.<br /><br /> Acepta valores NULL. Devuelve NULL si el evento no proporciona información adicional. |
| affected_rows | **bigint** | **Se aplica a**: La base de datos de SQL Azure solo<br /><br /> Número de filas afectadas por la instrucción ejecutada. |  
| application_name | **nvarchar(128)** | **Se aplica a**: Azure SQL DB + SQL Server (a partir de 2017)<br /><br /> Nombre de aplicación de cliente que ejecuta la instrucción que provocó el evento de auditoría |  
| audit_file_offset | **bigint** | **Se aplica a**: Sólo servidor SQL Server<br /><br /> Desplazamiento de búfer del archivo que contiene el registro de auditoría. No admite valores NULL. |  
| audit_schema_version | **int** | Siempre es 1 |  
| class_type | **varchar(2)** | El tipo de entidad auditable en la que se produce la auditoría. No admite valores NULL. |  
| client_ip | **nvarchar(128)** | **Se aplica a**: Azure SQL DB + SQL Server (a partir de 2017)<br /><br />    IP de la aplicación cliente de origen |  
| connection_id | GUID | **Se aplica a**: Instancia administrada y de base de datos SQL Azure<br /><br /> Identificador de la conexión en el servidor |
| data_sensitivity_information | nvarchar(4000) | **Se aplica a**: La base de datos de SQL Azure solo<br /><br /> Tipos de información y las etiquetas de confidencialidad devueltas por la consulta auditada, basándose en las columnas clasificadas en la base de datos. Obtenga más información sobre [clasificación y detección de datos de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification) |
| database_name | **sysname** | Contexto de base de datos en el que se produjo la acción. Acepta valores NULL. Devuelve NULL para las auditorías que se producen en el nivel de servidor. |  
| database_principal_id | **int** |Identificador del contexto de usuario de la base de datos en el que se realiza la acción. No admite valores NULL. Devuelve 0 si esto no es aplicable. Por ejemplo, una operación de servidor.|
| database_principal_name | **sysname** | Usuario actual. Acepta valores NULL. Devuelve NULL si no está disponible. |  
| duration_milliseconds | **bigint** | **Se aplica a**: Instancia administrada y de base de datos SQL Azure<br /><br /> Duración de la ejecución de consulta en milisegundos |
| event_time | **datetime2** | Fecha y hora cuando se desencadena la acción auditable. No admite valores NULL. |  
| file_name | **varchar(260)** | Ruta de acceso y nombre del archivo de registro de auditoría del que procede el registro. No admite valores NULL. |
| is_column_permission | **bit** | Marca que indica si éste es un permiso de nivel de columna. No admite valores NULL. Devuelve 0 si permission_bitmask = 0.<br /> 1 = verdadero<br /> 0 = falso |
| object_id | **int** | Identificador de la entidad en la que se produjo la auditoría. Incluye lo siguiente:<br /> Objetos de servidor<br /> Bases de datos<br /> Objetos de base de datos<br /> Objetos de esquema<br /> No admite valores NULL. Devuelve 0 si la entidad es el propio servidor o si la auditoría no se realiza en un nivel de objeto. Por ejemplo, la autenticación. |  
| object_name | **sysname** | El nombre de la entidad en la que se produjo la auditoría. Incluye lo siguiente:<br /> Objetos de servidor<br /> Bases de datos<br /> Objetos de base de datos<br /> Objetos de esquema<br /> Acepta valores NULL. Devuelve NULL si la entidad es el propio servidor o si la auditoría no se realiza en un nivel de objeto. Por ejemplo, la autenticación. |
| permission_bitmask | **varbinary (16)** | En algunas acciones, este es el permiso que se concedió, denegó o revocó. |
| response_rows | **bigint** | **Se aplica a**: Instancia administrada y de base de datos SQL Azure<br /><br /> Número de filas devueltas en el conjunto de resultados. |  
| schema_name | **sysname** | El contexto del esquema en el que se produjo la acción. Acepta valores NULL. Devuelve NULL para las auditorías que se producen fuera de un esquema. |  
| sequence_group_id | **varbinary** | **Se aplica a**: Sólo servidor SQL Server (a partir de 2016)<br /><br />  Identificador único |  
| sequence_number | **int** | Realiza un seguimiento de la secuencia de registros de un único registro de auditoría que era demasiado grande para caber en el búfer de escritura destinado a las auditorías. No admite valores NULL. |  
| server_instance_name | **sysname** | Nombre de la instancia de servidor donde se ha producido la auditoría. Se usa el formato servidor\instancia estándar. |  
| server_principal_id | **int** | Identificador del contexto de inicio de sesión en el que se realiza la acción. No admite valores NULL. |  
| server_principal_name | **sysname** | Inicio de sesión actual. Acepta valores NULL. |  
| server_principal_sid | **varbinary** | SID del inicio de sesión actual. Acepta valores NULL. |  
| session_id | **smallint** | Identificador de la sesión en la que se produjo el evento. No admite valores NULL. |  
| session_server_principal_name | **sysname** | Entidad de seguridad de servidor para la sesión. Acepta valores NULL. |  
| instrucción | **nvarchar(4000)** | Instrucción TSQL, si existe. Acepta valores NULL. Devuelve NULL si no es aplicable. |  
| succeeded | **bit** | Indica si la acción que desencadenó el evento se ha llevado a cabo correctamente. No admite valores NULL. Para todos los eventos que no sean los eventos de inicio de sesión, esto solo notifica si la comprobación del permiso tuvo o no tuvo éxito, no la operación.<br /> 1 = correcto<br /> 0 = error |
| target_database_principal_id | **int** | Entidad de seguridad de base de datos en la que se realiza la operación GRANT/DENY/REVOKE. No admite valores NULL. Devuelve 0 si no es aplicable. |  
| target_database_principal_name | **sysname** | Usuario de destino de la acción. Acepta valores NULL. Devuelve NULL si no es aplicable. |  
| target_server_principal_id | **int** | Entidad de seguridad de servidor en la que se realiza la operación GRANT/DENY/REVOKE. No admite valores NULL. Devuelve 0 si no es aplicable. |  
| target_server_principal_name | **sysname** | Inicio de sesión de destino de acción. Acepta valores NULL. Devuelve NULL si no es aplicable. |  
| target_server_principal_sid | **varbinary** | SID del inicio de sesión de destino. Acepta valores NULL. Devuelve NULL si no es aplicable. |  
| transaction_id | **bigint** | **Se aplica a**: Sólo servidor SQL Server (a partir de 2016)<br /><br /> Identificador único para identificar varios eventos de auditoría en una transacción |  
| user_defined_event_id | **smallint** | **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], instancia administrada y de base de datos de SQL Azure<br /><br /> Id. de evento definido por usuario se pasa como argumento a **sp_audit_write**. **NULL** para eventos del sistema (valor predeterminado) y distinto de cero para el evento definido por el usuario. Para obtener más información, consulte [sp_audit_write &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md). |  
| user_defined_information | **nvarchar(4000)** | **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], instancia administrada y de base de datos de SQL Azure<br /><br /> Permite registrar cualquier información adicional que el usuario desea grabar en el registro de auditoría mediante el **sp_audit_write** procedimiento almacenado. |  

  
## <a name="remarks"></a>Comentarios  
 Si el *file_pattern* argumento pasado a **fn_get_audit_file** hace referencia a una ruta de acceso o archivo que no existe, o si el archivo no es un archivo de auditoría, el **MSG_INVALID_AUDIT_FILE**devuelve el mensaje de error.  
  
## <a name="permissions"></a>Permisos

- **SQL Server**: Requiere el permiso **CONTROL SERVER** .  
- **Azure SQL DB**: Requiere el **CONTROL DATABASE** permiso.     
  - Los administradores de servidor pueden tener acceso a los registros de auditoría de todas las bases de datos en el servidor.
  - Servidor que no sean administradores solo pueden acceder a los registros de auditoría de la base de datos actual.
  - Se omitirán los blobs que no cumplen los criterios anteriores (se mostrará una lista de blobs omitidos en el mensaje de salida de consulta), y la función devolverá los registros solo de blobs para el que se permite el acceso.  
  
## <a name="examples"></a>Ejemplos

- **SQL Server**

  En este ejemplo se lee un archivo denominado `\\serverName\Audit\HIPAA_AUDIT.sqlaudit`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPAA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Azure SQL Database**

  Este ejemplo se lee desde un archivo denominado `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`:  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  Este ejemplo se lee desde el mismo archivo que el anterior, pero con cláusulas adicionales de T-SQL (**superior**, **ORDER BY**, y **donde** cláusula para filtrar los registros de auditoría devueltos por el función):
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  En este ejemplo lee todos los registros de los servidores que comienzan con de auditoría `Sh`: 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

Para ver un ejemplo completo de cómo crear una auditoría, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).

Para obtener información acerca de cómo configurar la auditoría de Azure SQL Database, consulte [empezar a trabajar con la auditoría de base de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-auditing).
  
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
  
  
