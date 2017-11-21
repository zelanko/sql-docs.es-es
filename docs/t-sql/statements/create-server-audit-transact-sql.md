---
title: "CREAR auditoría de servidor (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SERVER_AUDIT_TSQL
- SERVER AUDIT
- SERVER_AUDIT_TSQL
- CREATE SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- CREATE SERVER AUDIT statement
- audits [SQL Server], creating
ms.assetid: 1c321680-562e-41f1-8eb1-e7fa5ae45cc5
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bbeb32f18755a9ecd0bf57f094f0504b60f6eebf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-server-audit-transact-sql"></a>CREATE SERVER AUDIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un objeto de auditoría de servidor utilizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE SERVER AUDIT audit_name  
{  
    TO { [ FILE (<file_options> [ , ...n ] ) ] | APPLICATION_LOG | SECURITY_LOG }  
    [ WITH ( <audit_options> [ , ...n ] ) ]   
    [ WHERE <predicate_expression> ]  
}  
[ ; ]  
  
<file_options>::=  
{  
        FILEPATH = 'os_file_path'  
    [ , MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED } ]  
    [ , { MAX_ROLLOVER_FILES = { integer | UNLIMITED } } | { MAX_FILES = integer } ]  
    [ , RESERVE_DISK_SPACE = { ON | OFF } ]   
}  
  
<audit_options>::=  
{  
    [   QUEUE_DELAY = integer ]  
    [ , ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION } ]  
    [ , AUDIT_GUID = uniqueidentifier ]  
}  
  
<predicate_expression>::=  
{  
    [NOT ] <predicate_factor>   
    [ { AND | OR } [NOT ] { <predicate_factor> } ]   
    [,...n ]  
}  
  
<predicate_factor>::=   
    event_field_name { = | < > | ! = | > | > = | < | < = } { number | ' string ' }  
```  
  
## <a name="arguments"></a>Argumentos  
 TO { FILE | APPLICATION_LOG | SECURITY_LOG }  
 Determina la ubicación del destino de la auditoría. Las opciones son un archivo binario, registro de la aplicación de Windows o el registro de seguridad de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede escribir en el registro de seguridad de Windows sin configurar valores adicionales en Windows. Para obtener más información, vea [Escribir eventos de auditoría de SQL Server en el registro de seguridad](../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md).  
  
 FILEPATH ='*os_file_path*'  
 La ruta de acceso del registro de auditoría. El nombre de archivo se genera en función del nombre de la auditoría y del GUID de la auditoría.  
  
 MAXSIZE = { *max_size}*  
 Especifica el tamaño máximo que puede alcanzar el archivo de auditoría. El *max_size* valor debe ser un número entero seguido de MB, GB, TB o UNLIMITED. El tamaño mínimo que puede especificar para *max_size* 2 MB y el máximo es 2.147.483.647 TB. Si se especifica UNLIMITED, el archivo crecerá hasta que se llene el disco. (0 también indica UNLIMITED). Especificar un valor inferior a 2 MB, genera el error MSG_MAXSIZE_TOO_SMALL. El valor predeterminado es UNLIMITED.  
  
 MAX_ROLLOVER_FILES =*{entero* | ILIMITADO}  
 Especifica el número máximo de archivos que se deben conservar en el sistema de archivos además del archivo actual. El *MAX_ROLLOVER_FILES* valor debe ser un entero o UNLIMITED. El valor predeterminado es UNLIMITED. Este parámetro se evalúa cada vez que se reinicia la auditoría (lo que puede suceder cuando la instancia de la [!INCLUDE[ssDE](../../includes/ssde-md.md)] se reinicia o cuando se activa la auditoría off y, a continuación, en nuevo) o cuando se necesita un nuevo archivo porque se ha alcanzado el MAXSIZE. Cuando *MAX_ROLLOVER_FILES* se evalúa si el número de archivos supera el *MAX_ROLLOVER_FILES* establecer, el archivo más antiguo se elimina. Como resultado, cuando el valor de *MAX_ROLLOVER_FILES* es 0, se crea un nuevo archivo cada vez que la *MAX_ROLLOVER_FILES* se evalúa el valor. Solo un archivo automáticamente es eliminado al *MAX_ROLLOVER_FILES* se evalúa el valor, por lo que cuando el valor de *MAX_ROLLOVER_FILES* es ha disminuido, el número de archivos no se reduce a menos que sean archivos antiguos eliminar de forma manual. El número máximo de archivos que se pueden especificar es 2.147.483.647.  
  
 MAX_FILES =*entero*  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el número máximo de archivos de auditoría que pueden crearse. No realiza la sustitución incremental al primer archivo cuando se alcanza el límite. Cuando se alcanza el límite MAX_FILES, cualquier acción que ocasione la generación, de los eventos de auditoría adicionales produce un error.  
  
 RESERVE_DISK_SPACE = { ON | OFF }  
 Esta opción preasigna el archivo en el disco al valor de MAXSIZE. Se aplica solo si MAXSIZE no es igual a UNLIMITED. El valor predeterminado es OFF.  
  
 QUEUE_DELAY =*entero*  
 Determina el tiempo, en milisegundos, que puede transcurrir antes de que las acciones de auditoría se convierten obligatoriamente a procesarse. El valor 0 indica la entrega sincrónica. El valor mínimo que puede establecerse para la cola es 1000 (1 segundo), que es el valor predeterminado. El máximo es 2.147.483.647 (2.147.483,647 segundos, o 24 días, 20 horas, 31 minutos y 23,647 segundos). Especificar un número no válido, se genera el error MSG_INVALID_QUEUE_DELAY.  
  
 ON_FAILURE = {CONTINUAR | CIERRE | FAIL_OPERATION}  
 Indica si la escritura de la instancia en el destino debe suspender, continuar o detener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el destino no puede escribir en el registro de auditoría. El valor predeterminado es CONTINUE.  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Las operaciones de  continúan. Los registros de auditoría no se conservan. La auditoría continúa intentando registrar eventos y se reanudará si se resuelve la condición de error. Al seleccionar la opción continuar puede permitir que la actividad no auditada, lo que se infringirían las directivas de seguridad. Utilice esta opción cuando la operación de continuación del [!INCLUDE[ssDE](../../includes/ssde-md.md)] sea más importante que el mantenimiento de una auditoría completa.  
  
SHUTDOWN  
Obliga a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apagar, if [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se produce un error al escribir datos en el destino de auditoría por cualquier motivo. El inicio de sesión que ejecuta la `CREATE SERVER AUDIT` instrucción debe tener la `SHUTDOWN` permiso dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El comportamiento de apagado persiste incluso si la `SHUTDOWN` más adelante se revoca el permiso desde el inicio de sesión está ejecutando. Si el usuario no tiene este permiso, a continuación, la instrucción generará errores y la auditoría no se crea. Utilice la opción si un error de auditoría puede poner en peligro la seguridad o la integridad del sistema. Para obtener más información, consulte [apagado](../../t-sql/language-elements/shutdown-transact-sql.md).  
  
 FAIL_OPERATION  
 Las acciones de base de datos producen un error si generan eventos auditados. Las acciones, que no se producen eventos auditados pueden continuar, pero no los eventos auditados pueden producirse. La auditoría continúa intentando registrar eventos y se reanudará si se resuelve la condición de error. Utilice esta opción si el mantenimiento de una auditoría completa es más importante que el acceso total al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

 AUDIT_GUID =*uniqueidentifier*  
 Para que sea compatible con escenarios como la creación de reflejo de la base de datos, una auditoría necesita un GUID específico que coincida con el de la base de datos reflejada. No se puede modificar el GUID una vez creada la auditoría.  
  
 predicate_expression  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica la expresión de predicado usada para determinar si debe procesarse o no un evento. Las expresiones de predicado se limitan a 3.000 caracteres, lo que limita los argumentos de cadena.  
  
 event_field_name  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Es el nombre del campo de evento que identifica el origen del predicado. Campos de auditoría se describen en [sys.fn_get_audit_file &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). Todos los campos pueden auditarse excepto `file_name` y `audit_file_offset`.  
  
 number  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Es cualquier tipo numérico, incluido **decimal**. Las limitaciones son la falta de memoria física disponible o un número demasiado grande para ser representado como un entero de 64 bits.  
  
 ' string '  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Una cadena ANSI o Unicode según lo requerido por la comparación de predicado. No se realiza ninguna conversión implícita de tipos de cadena para las funciones de comparación de predicado. Si se pasa el tipo incorrecto se producirá un error.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se crea una auditoría de servidor, está en un estado deshabilitado.  
  
 La instrucción CREATE SERVER AUDIT está en el ámbito de una transacción. Si se revierte la transacción, también se revierte la instrucción.  
  
## <a name="permissions"></a>Permissions  
 Para crear, modificar o quitar una auditoría de servidor, las entidades de seguridad deben tener el permiso ALTER ANY SERVER AUDIT o CONTROL SERVER.  
  
 Al guardar información de auditoría en un archivo, para tratar de impedir su alteración, restrinja el acceso a la ubicación del archivo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-server-audit-with-a-file-target"></a>A. Crear una auditoría de servidor con destino a un archivo  
 En el ejemplo siguiente se crea una auditoría de servidor denominada `HIPPA_Audit` con un archivo binario como destino y sin ninguna opción.  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
```  
  
### <a name="b-creating-a-server-audit-with-a-windows-application-log-target-with-options"></a>B. Crear una auditoría de servidor con destino al registro de la aplicación Windows y con opciones  
 En el ejemplo siguiente se crea una auditoría de servidor denominada `HIPPA_Audit` con destino al registro de la aplicación Windows. La cola se escribe cada segundo y apaga el motor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se produce un error.  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO APPLICATION_LOG  
    WITH ( QUEUE_DELAY = 1000,  ON_FAILURE = SHUTDOWN);  
```  
  
###  <a name="ExampleWhere"></a> C. Crear un servidor de auditoría que contiene una cláusula WHERE  
 En el ejemplo siguiente se crean una base de datos, un esquema y dos tablas para el ejemplo. La tabla denominada `DataSchema.SensitiveData` contiene datos confidenciales y se registran en la auditoría de acceso a la tabla. La tabla denominada `DataSchema.GeneralData` no contiene datos confidenciales. La especificación de auditoría de base de datos audita el acceso a todos los objetos del esquema `DataSchema`. La auditoría de servidor se crea con una cláusula WHERE que limita la auditoría de servidor solamente a la tabla `SensitiveData`. La auditoría de servidor presupone que existe una carpeta de auditoría en `C:\SQLAudit`.  
  
```sql  
CREATE DATABASE TestDB;  
GO  
USE TestDB;  
GO  
CREATE SCHEMA DataSchema;  
GO  
CREATE TABLE DataSchema.GeneralData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
CREATE TABLE DataSchema.SensitiveData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
-- Create the server audit in the master database  
USE master;  
GO  
CREATE SERVER AUDIT AuditDataAccess  
    TO FILE ( FILEPATH ='C:\SQLAudit\' )  
    WHERE object_name = 'SensitiveData' ;  
GO  
ALTER SERVER AUDIT AuditDataAccess WITH (STATE = ON);  
GO  
-- Create the database audit specification in the TestDB database  
USE TestDB;  
GO  
CREATE DATABASE AUDIT SPECIFICATION [FilterForSensitiveData]  
FOR SERVER AUDIT [AuditDataAccess]   
ADD (SELECT ON SCHEMA::[DataSchema] BY [public])  
WITH (STATE = ON);  
GO  
-- Trigger the audit event by selecting from tables  
SELECT ID, DataField FROM DataSchema.GeneralData;  
SELECT ID, DataField FROM DataSchema.SensitiveData;  
GO  
-- Check the audit for the filtered content  
SELECT * FROM fn_get_audit_file('C:\SQLAudit\AuditDataAccess_*.sqlaudit',default,default);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREAR especificación de auditoría de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREAR especificación de auditoría de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [QUITE la especificación de auditoría de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Sys.fn_get_audit_file &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [Sys.server_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [Sys.server_file_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [Sys.server_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [Sys.server_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [Sys.database_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [Sys.database_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [Sys.dm_server_audit_status &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [Sys.dm_audit_actions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [Sys.dm_audit_class_type_map &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Crear una auditoría de servidor y una especificación de auditoría de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  

