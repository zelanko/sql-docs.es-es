---
title: Registros de SQL Server Audit | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audit records [SQL Server]
ms.assetid: 7a291015-df15-44fe-8d53-c6d90a157118
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3cc249ebfce796d7932e68d993ac98ede867845f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63238388"
---
# <a name="sql-server-audit-records"></a>SQL Server Audit Records
  La característica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit le permite auditar grupos de eventos y eventos de nivel de servidor y de base de datos. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](sql-server-audit-database-engine.md). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Las auditorías constan de cero o más elementos de acción de auditoría que se registran en un *destino*de auditoría. Este destino de auditoría puede ser un archivo binario, el registro de eventos de aplicación Windows o el registro de eventos de seguridad de Windows. Los registros que se envían al destino pueden contener los elementos descritos en la tabla siguiente.  
  
|Nombre de la columna|Descripción|Tipo|Siempre está disponible|  
|-----------------|-----------------|----------|----------------------|  
|**event_time**|Fecha y hora en la que se desencadena la acción auditable.|`datetime2`|Sí|  
|**sequence_no**|Realiza un seguimiento de la secuencia de registros de un único registro de auditoría que era demasiado grande para caber en el búfer de escritura destinado a las auditorías.|`int`|Sí|  
|**action_id**|Identificador de la acción.<br /><br /> Sugerencia: Para usar **action_id** como un predicado, debe convertirse de una cadena de caracteres a un valor numérico. Para obtener más información, vea [Filtrar SQL Server Audit por el predicado action_id / class_type](https://blogs.msdn.com/b/sqlsecurity/archive/2012/10/03/filter-sql-server-audit-on-action-id-class-type-predicate.aspx).|`varchar(4)`|Sí|  
|**completa**|Indica si la acción que desencadenó el evento se ha llevado a cabo correctamente|`bit`-1 = correcto, 0 = error|Sí|  
|**permission_bitmask**|Cuando es aplicable, muestra los permisos concedidos, denegados, o revocados.|`bigint`|No|  
|**is_column_permission**|Marca que especifica un permiso de nivel de columna|`bit`-1 = verdadero, 0 = falso|No|  
|**session_id**|Identificador de la sesión en la que se produjo el evento.|`int`|Sí|  
|**server_principal_id**|Identificador del contexto de inicio de sesión en el que se realiza la acción.|`int`|Sí|  
|**database_principal_id**|Identificador del contexto de usuario de la base de datos en el que se realiza la acción.|`int`|No|  
|**identificador de object_**|El identificador principal de la entidad en la que se produjo la auditoría. Esto incluye:<br /><br /> objetos de servidor<br /><br /> databases<br /><br /> Objetos de base de datos<br /><br /> objetos de esquema|`int`|No|  
|**target_server_principal_id**|Entidad de seguridad del servidor a la que se aplica la acción auditable.|`int`|Sí|  
|**target_database_principal_id**|Entidad de seguridad de la base de datos a la que se aplica la acción auditable.|`int`|No|  
|**class_type**|Tipo de entidad auditable en la que se produce la auditoría.|`varchar(2)`|Sí|  
|**session_server_principal_name**|Entidad de seguridad del servidor para la sesión.|`sysname`|Sí|  
|**server_principal_name**|Inicio de sesión actual.|`sysname`|Sí|  
|**server_principal_sid**|SID del inicio de sesión actual.|`varbinary`|Sí|  
|**database_principal_name**|Usuario actual.|`sysname`|No|  
|**target_server_principal_name**|Inicio de sesión de destino de la acción.|`sysname`|No|  
|**target_server_principal_sid**|SID del inicio de sesión de destino.|`varbinary`|No|  
|**target_database_principal_name**|Usuario de destino de la acción.|`sysname`|No|  
|**server_instance_name**|Nombre de la instancia de servidor donde se ha producido la auditoría. Usa el formato equipo\instancia estándar.|`nvarchar(120)`|Sí|  
|**database_name**|Contexto de base de datos en el que se produjo la acción.|`sysname`|No|  
|**schema_name**|Contexto de esquema en el que se produjo la acción.|`sysname`|No|  
|**object_name**|Nombre de la entidad en la que se produjo la auditoría. Esto incluye:<br /><br /> objetos de servidor<br /><br /> databases<br /><br /> Objetos de base de datos<br /><br /> objetos de esquema<br /><br /> Instrucción TSQL (si existe)|`sysname`|No|  
|**privacidad**|Instrucción TSQL (si existe)|`nvarchar(4000)`|No|  
|**additional_information**|Cualquier información adicional sobre el evento, almacenada como XML.|`nvarchar(4000)`|No|  
  
## <a name="remarks"></a>Observaciones  
 Algunas acciones no rellenan el valor de una columna porque es posible que no sea aplicable a la acción.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit almacena 4.000 caracteres de datos en los campos de carácter de un registro de auditoría. Si los valores **additional_information** y **statement** devueltos por una acción auditable contienen más de 4000 caracteres, la columna **sequence_no** se usa para escribir varios registros en el informe de auditoría para que una única acción de auditoría registre estos datos. El proceso es el siguiente:  
  
-   La columna **statement** se divide en 4.000 caracteres.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit escribe como primera fila del registro de auditoría los datos parciales. Los demás campos se duplican en cada fila.  
  
-   Se incrementa el valor **sequence_no** .  
  
-   Este proceso se repite hasta que se registran todos los datos.  
  
 Puede conectar los datos al leer las filas secuencialmente mediante el valor **sequence_no** , y las columnas **event_Time**, **action_id** y **session_id** para identificar la acción.  
  
## <a name="related-content"></a>Contenido relacionado  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)  
  
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-transact-sql)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-specification-transact-sql)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-transact-sql)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)  
  
  
