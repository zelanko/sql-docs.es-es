---
title: "EXECUTE AS (cláusula de Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AS
- AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permission sets [SQL Server]
- queues [SQL Server]
- stored procedures [SQL Server], executing
- user-defined functions [SQL Server], execution context
- EXECUTE AS
- triggers [SQL Server], execution context
- execution context [SQL Server]
- switching execution context
- functions [SQL Server], execution context
ms.assetid: bd517aa3-f06e-4356-87d8-70de5df4494a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: baf3fdc592265f1c2117ef3358820ae94ce8536c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="execute-as-clause-transact-sql"></a>EXECUTE AS (cláusula de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede definir el contexto de ejecución de los siguientes módulos definidos por el usuario: funciones (excepto funciones con valores de tabla insertadas), procedimientos, colas y desencadenadores.  
  
 Al especificar el contexto en el que se ejecuta el módulo, puede controlar qué cuenta de usuario de la [!INCLUDE[ssDE](../../includes/ssde-md.md)] se utiliza para validar permisos en objetos que hace referencia el módulo. De esta forma se dispone de mayor control y flexibilidad para administrar los permisos a lo largo de la cadena de objetos que existe entre los módulos definidos por el usuario y los objetos a los que esos módulos hacen referencia. Los permisos deben concederse a usuarios únicamente del propio módulo, sin tener que concederles permisos explícitos para los objetos referenciados. Solo el usuario que ejecuta el módulo debe tener permisos en los objetos a los que tiene acceso el módulo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- SQL Server Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }   
  
DDL Triggers with Server Scope and logon triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'login_name' }   
  
Queues  
{ EXEC | EXECUTE } AS { SELF | OWNER | 'user_name' }   
```  
  
```  
  
-- Windows Azure SQL Database Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 **AUTOR DE LLAMADA**  
 Especifica que las instrucciones dentro del módulo se ejecutan en el contexto del llamador del módulo. El usuario que ejecuta el módulo debe tener los permisos adecuados no solo en el propio módulo, sino también en los objetos de la base de datos a los que el módulo hace referencia.  
  
 CALLER es el valor predeterminado para todos los módulos excepto las colas, y tiene el mismo comportamiento que [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 CALLER no se puede especificar en una instrucción CREATE QUEUE o ALTER QUEUE.  
  
 **EN SÍ MISMO**  
 EXECUTE AS SELF es equivalente a EXECUTE AS *nombre_usuario*, donde el usuario especificado es la persona que crea o modifica el módulo. El identificador de usuario real de la persona que crea o modifica los módulos se almacena en la **execute_as_principal_id** columna en el **sys.sql_modules** o **sys.service_queues** vista de catálogo.  
  
 SELF es el valor predeterminado para colas.  
  
> [!NOTE]  
>  Para cambiar el identificador de usuario de la **execute_as_principal_id** en el **sys.service_queues** vista de catálogo debe especificar explícitamente la ejecución como opción en la instrucción ALTER QUEUE.  
  
 OWNER  
 Especifica que las instrucciones dentro del módulo se ejecutan en el contexto del propietario actual del módulo. Si el módulo no tiene un propietario especificado, se usa el propietario del esquema del módulo. OWNER no se puede especificar para los desencadenadores DDL o logon.  
  
> [!IMPORTANT]  
>  OWNER debe asignarse a una cuenta singleton y no puede ser un rol o un grupo.  
  
 **'** *nombre_usuario* **'**  
 Especifica que las instrucciones dentro del módulo que se ejecutan en el contexto del usuario especificado en *nombre_usuario*. Los permisos para los objetos dentro del módulo se comprueban con *nombre_usuario*. *user_name* no se puede especificar para desencadenadores DDL con desencadenadores de ámbito o inicio de sesión del servidor. Use *login_name* en su lugar.  
  
 *user_name* debe existir en la base de datos actual y debe ser una cuenta singleton. *user_name* no puede ser un grupo, rol, certificado, clave o cuenta integrada, como NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService o NT AUTHORITY\LocalSystem.  
  
 El identificador de usuario del contexto de ejecución se almacena en los metadatos y puede verse en la **execute_as_principal_id** columna en el **sys.sql_modules** o **sys.assembly_modules** vista de catálogo.  
  
 **'** *login_name* **'**  
 Especifica que las instrucciones dentro del módulo que se ejecutan en el contexto de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión especificado en *login_name*. Los permisos para los objetos dentro del módulo se comprueban con *login_name*. *login_name* puede especificarse únicamente para desencadenadores DDL con desencadenadores de ámbito o inicio de sesión del servidor.  
  
 *login_name* no puede ser un grupo, rol, certificado, clave o cuenta integrada, como NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService o NT AUTHORITY\LocalSystem.  
  
## <a name="remarks"></a>Comentarios  
 Como [!INCLUDE[ssDE](../../includes/ssde-md.md)] evalúa los permisos en los objetos a los que el módulo hace referencia, depende de la cadena de propiedad que existe entre los objetos que llaman y los objetos a los que se hace referencia. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la cadena de propiedad era el único método disponible para evitar tener que conceder al usuario que llama acceso a todos los objetos a los que se hace referencia.  
  
 La cadena de propiedad tiene las siguientes limitaciones:  
  
-   Solo se aplica a instrucciones DML: SELECT, INSERT, UPDATE y DELETE.  
  
-   Los propietarios de los objetos que llaman y llamados deben ser los mismos.  
  
-   No se aplica a consultas dinámicas dentro del módulo.  
  
 Independientemente del contexto de ejecución especificado en el módulo, siempre se aplican las siguientes acciones:  
  
-   Cuando se ejecuta el módulo, [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba primero que el usuario que ejecuta el módulo tiene el permiso EXECUTE en el módulo.  
  
-   Las reglas de la cadena de propiedad siguen aplicándose. Esto significa que si los propietarios de los objetos que llaman y llamados son los mismos, no se comprueban los permisos en los objetos subyacentes.  
  
 Cuando un usuario ejecuta un módulo que se ha especificado para ejecutar en un contexto distinto de CALLER, se comprueba el permiso del usuario para ejecutar el módulo, pero también se realizan comprobaciones adicionales de permisos en objetos a los que tiene acceso el módulo contra la cuenta de usuario especificada en la cláusula EXECUTE AS. El usuario que ejecuta el módulo suplanta al usuario especificado.  
  
 El contexto especificado en la cláusula EXECUTE AS del módulo solo es válido durante la ejecución del módulo. El contexto vuelve al llamador cuando finaliza la ejecución del módulo.  
  
## <a name="specifying-a-user-or-login-name"></a>Especificar un nombre de inicio de sesión o usuario  
 Un usuario de base de datos o un inicio de sesión de servidor especificado en la cláusula EXECUTE AS de un módulo no puede quitarse hasta que el módulo se haya modificado para ejecutarse en otro contexto.  
  
 El nombre de usuario o inicio de sesión especificado en la cláusula EXECUTE AS debe existir como entidad de seguridad en **sys.database_principals** o **sys.server_principals**, respectivamente, o crear o modificar el error de la operación de módulo . Además, el usuario que crea o modifica el módulo debe tener permisos IMPERSONATE en la entidad de seguridad.  
  
 Si el usuario tiene acceso implícito a la base de datos o instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] porque pertenece a un grupo de Windows, el usuario especificado en la cláusula EXECUTE AS se crea de forma implícita cuando se crea el módulo y se cumple uno de los siguientes requisitos:  
  
-   El usuario especificado o el inicio de sesión es un miembro de la **sysadmin** rol fijo de servidor.  
  
-   El usuario que crea el módulo tiene permiso para crear entidades de seguridad.  
  
 Cuando no se cumple ninguno de esos requisitos, la operación de creación del módulo genera errores.  
  
> [!IMPORTANT]  
>  Si el servicio (MSSQLSERVER) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutándose como una cuenta local (servicio local o cuenta de usuario local), no tendrá privilegios para obtener la pertenencia a grupo de una cuenta de dominio de Windows especificada en la cláusula EXECUTE AS. Esto generará errores en la ejecución del módulo.  
  
 Por ejemplo, supongamos las siguientes condiciones:  
  
-   **CompanyDomain\SQLUsers** grupo tiene acceso a la **ventas** base de datos.  
  
-   **CompanyDomain\SqlUser1** es un miembro de **SQLUsers** y, por lo tanto, tiene acceso a la **ventas** base de datos.  
  
-   El usuario que crea o modifica el módulo tiene permisos para crear entidades de seguridad.  
  
 Cuando se ejecute la siguiente instrucción `CREATE PROCEDURE`, el `CompanyDomain\SqlUser1` se crea de forma implícita como una entidad de seguridad de la base de datos en la base de datos `Sales`.  
  
```  
USE Sales;  
GO  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'CompanyDomain\SqlUser1'  
AS  
SELECT user_name();  
GO  
```  
  
## <a name="using-execute-as-caller-stand-alone-statement"></a>Usar la instrucción independiente EXECUTE AS CALLER  
 Use la instrucción independiente EXECUTE AS CALLER dentro de un módulo para establecer el contexto de ejecución al llamador del módulo.  
  
 Suponga que `SqlUser2` llama al siguiente procedimiento almacenado.  
  
```  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'SqlUser1'  
AS  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
EXECUTE AS CALLER;  
SELECT user_name(); -- Shows execution context is set to SqlUser2, the caller of the module.  
REVERT;  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
GO  
```  
  
## <a name="using-execute-as-to-define-custom-permission-sets"></a>Usar EXECUTE AS para definir conjuntos de permisos personalizados  
 Cuando desee definir conjuntos de permisos personalizados puede ser muy útil especificar un contexto de ejecución para un módulo. Por ejemplo, algunas acciones, como TRUNCATE TABLE, no tienen permisos que se puedan conceder. Al incorporar la instrucción TRUNCATE TABLE en un módulo y especificar que ese módulo se ejecute con un usuario que tiene permisos para modificar la tabla, puede ampliar los permisos para truncar la tabla al usuario a quien ha concedido permisos EXECUTE para el módulo.  
  
 Para ver la definición del módulo con el contexto de ejecución especificado, utilice la [sys.sql_modules &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) vista de catálogo.  
  
## <a name="best-practice"></a>Práctica recomendada  
 Especifique un inicio de sesión o usuario que tenga al menos los privilegios requeridos para realizar las operaciones definidas en el módulo. Por ejemplo, no especifique una cuenta de propietario de base de datos a menos que tenga los permisos requeridos.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar un módulo especificado con EXECUTE AS, el llamador debe tener permisos EXECUTE en el módulo.  
  
 Para ejecutar un módulo CLR especificado con EXECUTE AS que tiene acceso a recursos en otra base de datos o servidor, la base de datos o el servidor de destino deben confiar en el autenticador de la base de datos que ha originado el módulo (la base de datos de origen).  
  
 Para especificar la cláusula EXECUTE AS cuando cree o modifique un módulo, debe tener permisos IMPERSONATE en la entidad de seguridad especificada y, además, permisos para crear el módulo. Siempre puede suplantarse a usted mismo. Cuando no se especifica ningún contexto de ejecución o se especifica EXECUTE AS CALLER, no se requieren permisos IMPERSONATE.  
  
 Para especificar un *login_name* o *nombre_usuario* que tiene acceso implícito a la base de datos a través de la pertenencia a un grupo de Windows, debe tener permisos de CONTROL en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea un procedimiento almacenado en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] y se asigna el contexto de ejecución a `OWNER`.  
  
```  
CREATE PROCEDURE HumanResources.uspEmployeesInDepartment   
@DeptValue int  
WITH EXECUTE AS OWNER  
AS  
    SET NOCOUNT ON;  
    SELECT e.BusinessEntityID, c.LastName, c.FirstName, e.JobTitle  
    FROM Person.Person AS c   
    INNER JOIN HumanResources.Employee AS e  
        ON c.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS edh  
        ON e.BusinessEntityID = edh.BusinessEntityID  
    WHERE edh.DepartmentID = @DeptValue  
    ORDER BY c.LastName, c.FirstName;  
GO  
  
-- Execute the stored procedure by specifying department 5.  
EXECUTE HumanResources.uspEmployeesInDepartment 5;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Sys.service_queues &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-service-queues-transact-sql.md)   
 [REVERTIR &#40; Transact-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EJECUTAR AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
