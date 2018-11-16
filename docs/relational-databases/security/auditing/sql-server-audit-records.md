---
title: Registros de SQL Server Audit | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audit records [SQL Server]
ms.assetid: 7a291015-df15-44fe-8d53-c6d90a157118
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c657e42e1e754ca843a40967221512f55c9c9c9f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675344"
---
# <a name="sql-server-audit-records"></a>SQL Server Audit Records
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La característica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit le permite auditar grupos de eventos y eventos de nivel de servidor y de base de datos. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Las auditorías constan de cero o más elementos de acción de auditoría que se registran en un *destino*de auditoría. Este destino de auditoría puede ser un archivo binario, el registro de eventos de aplicación Windows o el registro de eventos de seguridad de Windows. Los registros que se envían al destino pueden contener los elementos descritos en la tabla siguiente:  
  
|Nombre de columna|Descripción|Tipo|Siempre está disponible|  
|-----------------|-----------------|----------|----------------------|  
|**event_time**|Fecha y hora en la que se desencadena la acción auditable.|**datetime2**|Sí|  
|**sequence_no**|Realiza un seguimiento de la secuencia de registros de un único registro de auditoría que era demasiado grande para caber en el búfer de escritura destinado a las auditorías.|**int**|Sí|  
|**action_id**|Id. de la acción<br /><br /> Sugerencia: Para usar **action_id** como un predicado, debe convertirse de una cadena de caracteres a un valor numérico. Para obtener más información, vea [Filtrar SQL Server Audit por el predicado action_id / class_type](https://blogs.msdn.com/b/sqlsecurity/archive/2012/10/03/filter-sql-server-audit-on-action-id-class-type-predicate.aspx).|**varchar(4)**|Sí|  
|**succeeded**|Indica si la comprobación del permiso de la acción que desencadena el evento de auditoría se ha realizado correctamente o no. |**bit**<br /> – 1 = correcto, <br />0 = error|Sí|  
|**permission_bitmask**|Si procede, muestra los permisos que se han concedido, denegado o revocado|**bigint**|no|  
|**is_column_permission**|Marca que especifica un permiso de nivel de columna|**bit** <br />– 1 = True, <br />0 = False|no|  
|**session_id**|Identificador de la sesión en la que se produjo el evento.|**int**|Sí|  
|**server_principal_id**|Identificador del contexto de inicio de sesión en el que se realiza la acción.|**int**|Sí|  
|**database_principal_id**|Identificador del contexto de usuario de la base de datos en el que se realiza la acción.|**int**|no|  
|**object_id**|El identificador principal de la entidad en la que se produjo la auditoría. Este identificador puede ser:<br /><br /> objetos de servidor<br /><br /> bases de datos<br /><br /> objetos de base de datos<br /><br /> objetos de esquema|**int**|no|  
|**target_server_principal_id**|Entidad de seguridad del servidor a la que se aplica la acción auditable.|**int**|Sí|  
|**target_database_principal_id**|Entidad de seguridad de la base de datos a la que se aplica la acción auditable.|**int**|no|  
|**class_type**|Tipo de entidad auditable en la que se produce la auditoría.|**varchar(2)**|Sí|  
|**session_server_principal_name**|Entidad de seguridad del servidor para la sesión.|**sysname**|Sí|  
|**server_principal_name**|Inicio de sesión actual.|**sysname**|Sí|  
|**server_principal_sid**|SID del inicio de sesión actual.|**varbinary**|Sí|  
|**database_principal_name**|Usuario actual.|**sysname**|no|  
|**target_server_principal_name**|Inicio de sesión de destino de la acción.|**sysname**|no|  
|**target_server_principal_sid**|SID del inicio de sesión de destino.|**varbinary**|no|  
|**target_database_principal_name**|Usuario de destino de la acción.|**sysname**|no|  
|**server_instance_name**|Nombre de la instancia de servidor donde se ha producido la auditoría. Usa el formato equipo\instancia estándar.|**nvarchar(120)**|Sí|  
|**database_name**|Contexto de base de datos en el que se produjo la acción.|**sysname**|no|  
|**schema_name**|El contexto del esquema en el que se produjo la acción.|**sysname**|no|  
|**object_name**|El nombre de la entidad en la que se produjo la auditoría. Este nombre puede ser:<br /><br /> objetos de servidor<br /><br /> bases de datos<br /><br /> objetos de base de datos<br /><br /> objetos de esquema<br /><br /> Instrucción TSQL (si existe)|**sysname**|no|  
|**instrucción**|Instrucción TSQL (si existe)|**nvarchar(4000)**|no|  
|**additional_information**|Cualquier información adicional sobre el evento, almacenada como XML.|**nvarchar(4000)**|no|  
  
## <a name="remarks"></a>Notas  
 Algunas acciones no rellenan el valor de una columna porque es posible que no sea aplicable a la acción.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit almacena 4.000 caracteres de datos en los campos de carácter de un registro de auditoría. Si los valores **additional_information** y **statement** devueltos por una acción auditable contienen más de 4000 caracteres, la columna **sequence_no** se usa para escribir varios registros en el informe de auditoría para que una única acción de auditoría registre estos datos. El proceso es el siguiente:  
  
-   La columna **statement** se divide en 4.000 caracteres.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit escribe como primera fila del registro de auditoría los datos parciales. Los demás campos se duplican en cada fila.  
  
-   Se incrementa el valor **sequence_no** .  
  
-   Este proceso se repite hasta que se registran todos los datos.  
  
 Puede conectar los datos al leer las filas secuencialmente mediante el valor **sequence_no** , y las columnas **event_Time**, **action_id** y **session_id** para identificar la acción.  
  
## <a name="related-content"></a>Contenido relacionado  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-transact-sql.md)  
  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-transact-sql.md)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-authorization-transact-sql.md)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)  
  
  
