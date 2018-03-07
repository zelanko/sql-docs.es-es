---
title: GRANT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GRANT_TSQL
- GRANT
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], GRANT statement
- schema-level securables [SQL Server]
- GRANT statement
- cross-database permissions
- GRANT statement, about GRANT statement
- server-level securables [SQL Server]
- database-level securables [SQL Server]
- permissions [SQL Server], granting
ms.assetid: a760c16a-4d2d-43f2-be81-ae9315f38185
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 618e2068c1b1e9b99a68d0216c17c66e9b2cf3d1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="grant-transact-sql"></a>GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concede permisos sobre un elemento protegible a una entidad de seguridad.  El concepto general es GRANT \<algún permiso > ON \<algún objeto > TO \<algún usuario, inicio de sesión o grupo >. Para obtener una descripción general de los permisos, consulte [permisos &#40; motor de base de datos &#41;](../../relational-databases/security/permissions-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for GRANT  
GRANT { ALL [ PRIVILEGES ] }  
      | permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      [ ON [ class :: ] securable ] TO principal [ ,...n ]   
      [ WITH GRANT OPTION ] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 ALL  
 Esta opción ha quedado desusada y solo se mantiene por razones de compatibilidad con versiones anteriores. No concede todos los permisos posibles. Conceder ALL es equivalente a conceder los siguientes permisos.  
  
-   Si el elemento protegible es una base de datos, ALL significa BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE y CREATE VIEW.  
  
-   Si el elemento protegible es una función escalar, ALL significa EXECUTE y REFERENCES.  
  
-   Si el elemento protegible es una función con valores de tabla, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
-   Si el elemento protegible es un procedimiento almacenado, ALL significa EXECUTE.  
  
-   Si el elemento protegible es una tabla, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
-   Si el elemento protegible es una vista, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
PRIVILEGES  
 Incluido por compatibilidad con ISO. No cambia el comportamiento de ALL.  
  
*permiso*  
 Es el nombre de un permiso. Las asignaciones de permisos válidas a elementos protegibles se describen en los subtemas que se muestran a continuación.  
  
*columna*  
 Especifica el nombre de una columna de una tabla en la que se van a conceder los permisos. Los paréntesis () son obligatorios.  
  
*clase*  
 Especifica la clase del elemento protegible en el que se va a conceder el permiso. El calificador de ámbito **::** es necesario.  
  
*elemento protegible*  
 Especifica el elemento protegible para el que se va a conceder el permiso.  
  
PARA *principal*  
 Es el nombre de una entidad de seguridad. Las entidades de seguridad a las que se pueden conceder permisos para un elemento protegible varían según el elemento protegible. Vea los subtemas enumerados a continuación para comprobar las combinaciones válidas.  
  
GRANT OPTION  
 Indica que el receptor también podrá conceder el permiso especificado a otras entidades de seguridad.  
  
AS *principal*  
 Utilice la cláusula AS principal para indicar que la entidad de seguridad ha registrado como el otorgante del permiso debe ser una entidad de seguridad que no sea la persona que ejecuta la instrucción. Por ejemplo, suponga que el usuario Mary es principal_id 12 y usuario Raul es 15 principal. Mary ejecuta `GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` ahora en la tabla sys.database_permissions indicará que el grantor_prinicpal_id fue 15 (Raul), aunque la instrucción se ejecutó realmente por usuario 13 (Mary).

La cláusula AS normalmente no se recomienda utilizar a menos que necesite definir explícitamente la cadena de permiso. Para obtener más información, consulte el **resumen del algoritmo de comprobación de permiso** sección de [permisos (motor de base de datos)](../../relational-databases/security/permissions-database-engine.md).

El uso de como en esta instrucción no implica la capacidad de suplantar a otro usuario. 
  
## <a name="remarks"></a>Comentarios  
 La sintaxis completa de la instrucción GRANT es compleja. El diagrama de sintaxis anterior se ha simplificado para concentrar la atención en su estructura. La sintaxis completa para conceder permisos para elementos protegibles específicos se describe en los temas enumerados a continuación.  
  
 Se puede utilizar la instrucción REVOKE para retirar permisos concedidos y la instrucción DENY para evitar que una entidad de seguridad obtenga un permiso específico mediante una instrucción GRANT.  
  
 La concesión de un permiso quita DENY o REVOKE de ese permiso para el elemento protegible especificado. Si se deniega el mismo permiso en un ámbito superior que contiene el elemento protegible, DENY tiene prioridad. No obstante, revocar el permiso concedido en un ámbito superior no tiene prioridad.  
  
 Los permisos de nivel de base de datos se conceden en el ámbito de la base de datos especificada. Si un usuario necesita permisos para objetos de otra base de datos, cree la cuenta del usuario en la otra base de datos o conceda a la cuenta del usuario acceso a la otra base de datos y a la base de datos actual.  
  
> [!CAUTION]  
>  Un permiso DENY de nivel de tabla no tiene prioridad sobre uno GRANT de nivel de columna. Esta incoherencia en la jerarquía de permisos se ha mantenido por motivos de compatibilidad con versiones anteriores. Se quitará en una versión futura.  
  
 El sistema sp_helprotect almacenados procedimiento informa de los permisos en un elemento protegible de nivel de base de datos.  
  
## <a name="with-grant-option"></a>WITH GRANT OPTION  
 El **GRANT** ... **CON GRANT OPTION** especifica que la entidad de seguridad que recibe el permiso tiene la capacidad de conceder el permiso especificado a otras cuentas de seguridad. Cuando la entidad de seguridad que recibe el permiso es un rol o un grupo de Windows, la **AS** cláusula debe usarse cuando el permiso de objeto debe ser más concedido a los usuarios que no son miembros del grupo o del rol. Dado que sólo un usuario, en lugar de un grupo o función, puede ejecutar una **GRANT** instrucción, un miembro específico del grupo o rol debe usar el **AS** cláusula para invocar explícitamente la pertenencia al rol o grupo al conceder el permiso. El siguiente ejemplo se muestra cómo el **WITH GRANT OPTION** se utiliza cuando se concede a un rol o grupo de Windows.  
  
```  
-- Execute the following as a database owner  
GRANT EXECUTE ON TestProc TO TesterRole WITH GRANT OPTION;  
EXEC sp_addrolemember TesterRole, User1;  
-- Execute the following as User1  
-- The following fails because User1 does not have the permission as the User1  
GRANT EXECUTE ON TestMe TO User2;  
-- The following succeeds because User1 invokes the TesterRole membership  
GRANT EXECUTE ON TestMe TO User2 AS TesterRole;  
```  
  
## <a name="chart-of-sql-server-permissions"></a>Gráfico de los permisos de SQL Server  
 Para obtener un gráfico con tamaño cartel de todos los permisos del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en formato PDF, vea [http://go.microsoft.com/fwlink/?LinkId=229142](http://go.microsoft.com/fwlink/?LinkId=229142).  
  
## <a name="permissions"></a>Permissions  
 El otorgante del permiso (o la entidad de seguridad especificada con la opción AS) debe tener el permiso con GRANT OPTION, o un permiso superior que implique el permiso que se va a conceder. Si se utiliza la opción AS, se aplican requisitos adicionales. Para obtener más detalles vea el tema específico de los elementos protegibles.  
  
 Los propietarios de objetos pueden conceder permisos para los objetos que poseen. Las entidades de seguridad con permiso CONTROL sobre un elemento protegible pueden conceder permisos para ese elemento.  
  
 Los receptores del permiso CONTROL SERVER como los miembros del rol fijo de servidor sysadmin pueden conceder los permisos sobre cualquier elemento protegible en el servidor. Los receptores del permiso CONTROL para una base de datos, como los miembros del rol fijo de base de datos db_owner, pueden conceder los permisos para cualquier elemento protegible en la base de datos. Los receptores del permiso CONTROL en un esquema pueden conceder los permisos en cualquier objeto del esquema.  
  
## <a name="examples"></a>Ejemplos  
 En la tabla siguiente se enumera los elementos protegibles y los temas que describen la sintaxis específica de los mismos.  
  
|||  
|-|-|  
|Rol de aplicación|[CONCEDER permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Ensamblado|[CONCEDER permisos de ensamblado &#40; Transact-SQL &#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|Clave asimétrica|[CONCEDER permisos de clave asimétrica &#40; Transact-SQL &#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidad|[Permisos de grupo de disponibilidad de GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|Certificado|[Permisos de certificado GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|Contrato|[Permisos de concesión Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Base de datos|[Permisos de base de datos GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|Credencial con ámbito de base de datos|[Ámbito de base de datos de concesión de credenciales (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|Extremo|[CONCEDER permisos de extremo &#40; Transact-SQL &#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|Catálogo de texto completo|[Permisos de texto completo de GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Lista de palabras irrelevantes de texto completo|[Permisos de texto completo de GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Función|[Permisos de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Inicio de sesión|[CONCEDER permisos de entidad de seguridad de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|Tipo de mensaje|[Permisos de concesión Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Object|[Permisos de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Cola|[Permisos de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Enlace de servicio remoto|[Permisos de concesión Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Rol|[CONCEDER permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Ruta|[Permisos de concesión Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|esquema|[CONCEDER permisos de esquema &#40; Transact-SQL &#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|Lista de propiedades de búsqueda|[Permisos de lista de propiedades de búsqueda de GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|Server|[GRANT &#40;permisos de servidor de Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|ssNoVersion|[Permisos de concesión Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Procedimiento almacenado|[Permisos de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Clave simétrica|[CONCEDER permisos de clave simétrica &#40; Transact-SQL &#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|Synonym (Sinónimo)|[Permisos de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Objetos de sistema|[Permisos de objeto de sistema GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|Tabla|[Permisos de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Tipo|[Tipo de concesión de permisos &#40; Transact-SQL &#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|Usuario|[CONCEDER permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Ver|[Permisos de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Colección de esquemas XML|[CONCEDER permisos de colección de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Vea también  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
