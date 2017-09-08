---
title: DENY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DENY
- DENY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- security [SQL Server], denying access
- DENY statement
- permissions [SQL Server], denying
- server-level securables [SQL Server]
- inherited security settings [SQL Server]
- denying permissions [SQL Server], DENY statement
- principal security [SQL Server]
- database-level securables [SQL Server]
- denying permissions [SQL Server]
ms.assetid: c32d1e01-9ee9-4665-a516-fcfece58078e
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 08f2d3c555dceef71e331b6df8727afb5780b86b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="deny-transact-sql"></a>DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Deniega un permiso a una entidad de seguridad. Evita que la entidad de seguridad herede permisos por su pertenencia a grupos o roles. DENY tiene prioridad sobre todos los permisos, salvo que no se aplica a los propietarios de objetos o miembros del rol fijo de servidor sysadmin.
  **Nota de seguridad** miembros del rol sysadmin rol fijo de servidor y no se puede denegar permisos a los propietarios de objetos. "
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for DENY  
DENY   { ALL [ PRIVILEGES ] } 
     | <permission>  [ ( column [ ,...n ] ) ] [ ,...n ]  
    [ ON [ <class> :: ] securable ] 
    TO principal [ ,...n ]   
    [ CASCADE] [ AS principal ]  
[;]

<permission> ::=  
{ see the tables below }  
  
<class> ::=  
{ see the tables below }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class> ::=  
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
 Esta opción no deniega todos los permisos posibles. Al denegar ALL se deniegan los permisos siguientes.  
  
-   Si el elemento protegible es una base de datos, ALL significa BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE y CREATE VIEW.  
  
-   Si el elemento protegible es una función escalar, ALL significa EXECUTE y REFERENCES.  
  
-   Si el elemento protegible es una función con valores de tabla, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
-   Si el elemento protegible es un procedimiento almacenado, ALL significa EXECUTE.  
  
-   Si el elemento protegible es una tabla, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
-   Si el elemento protegible es una vista, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
> [!NOTE]  
>  La sintaxis de DENY ALL está desusada. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, deniegue permisos concretos.  
  
 PRIVILEGES  
 Incluido por compatibilidad con ISO. No cambia el comportamiento de ALL.  
  
 *permiso*  
 Es el nombre de un permiso. Las asignaciones de permisos válidas a elementos protegibles se describen en los subtemas que se muestran a continuación.  
  
 *columna*  
 Especifica el nombre de una columna de una tabla para la que se deniegan los permisos. Los paréntesis () son obligatorios.  
  
 *clase*  
 Especifica la clase de elemento protegible para el que se deniega el permiso. El calificador de ámbito **::** es necesario.  
  
 *elemento protegible*  
 Especifica el elemento protegible para el que se deniega el permiso.  
  
 PARA *principal*  
 Es el nombre de una entidad de seguridad. Las entidades de seguridad para las que se pueden denegar permisos sobre un elemento protegible varían en función de este elemento protegible. Vea los temas sobre elementos protegibles enumerados más abajo para obtener combinaciones válidas.  
  
 CASCADE  
 Indica que el permiso se deniega para la entidad de seguridad especificada y para el resto de entidades de seguridad a las que ésta concedió el permiso. Es obligatorio cuando la entidad de seguridad tiene el permiso con GRANT OPTION.  
  
 AS *principal*  
  Utilice la cláusula AS principal para indicar que la entidad de seguridad ha registrado como el denier del permiso debe ser una entidad de seguridad que no sea la persona que ejecuta la instrucción. Por ejemplo, suponga que el usuario Mary es principal_id 12 y usuario Raul es 15 principal. Mary ejecuta `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` ahora en la tabla sys.database_permissions indicará que el grantor_prinicpal_id de la instrucción deny fue 15 (Raul), aunque la instrucción se ejecutó realmente por usuario 13 (Mary).
  
El uso de como en esta instrucción no implica la capacidad de suplantar a otro usuario.  
  
## <a name="remarks"></a>Comentarios  
 La sintaxis completa de la instrucción DENY es compleja. El diagrama de sintaxis anterior se ha simplificado para concentrar la atención en su estructura. La sintaxis completa para denegar permisos sobre elementos protegibles específicos se describe en los temas enumerados más adelante.  
  
 DENY producirá un error si CASCADE no se especifica al denegar un permiso a una entidad de seguridad a la que se concedió ese permiso con GRANT OPTION.  
  
 El sistema sp_helprotect almacenados procedimiento informa de los permisos en un elemento protegible de nivel de base de datos.  
  
> [!CAUTION]  
>  Un permiso DENY de nivel de tabla no tiene prioridad sobre uno GRANT de nivel de columna. Esta incoherencia en la jerarquía de permisos se ha mantenido por motivos de compatibilidad con versiones anteriores. Se quitará en una versión futura.  
  
> [!CAUTION]  
>  Si se deniega el permiso CONTROL para una base de datos, se deniega implícitamente el permiso CONNECT para la misma. Una entidad de seguridad a la que se deniega el permiso CONTROL para una base de datos no podrá conectarse a esa base de datos.  
  
> [!CAUTION]  
>  Si se deniega el permiso CONTROL SERVER, se deniega implícitamente el permiso CONNECT SQL para el servidor. Una entidad de seguridad a la que se deniega el permiso CONTROL SERVER para un servidor no podrá conectarse a ese servidor.  
  
## <a name="permissions"></a>Permissions  
 El autor de la llamada (o la entidad de seguridad especificada en la opción AS) debe tener el permiso CONTROL sobre el elemento protegible o un permiso superior que implique el permiso CONTROL sobre el elemento protegible. Si utiliza la opción AS, la entidad de seguridad especificada debe poseer el elemento protegible sobre el que se deniega un permiso.  
  
 Los beneficiarios del permiso CONTROL SERVER, por ejemplo, los miembros del rol fijo de servidor sysadmin, pueden denegar cualquier permiso sobre cualquier elemento protegible en el servidor. Los beneficiarios del permiso CONTROL en la base de datos, por ejemplo, los miembros del rol fijo de base de datos db_owner, pueden denegar cualquier permiso sobre cualquier elemento protegible en la base de datos. Los beneficiarios del permiso CONTROL sobre un esquema pueden denegar cualquier permiso sobre cualquier objeto en el esquema. Si se usa la cláusula AS, la entidad de seguridad especificada debe ser propietaria del elemento protegible cuyos permisos que se van a denegar.  
  
## <a name="examples"></a>Ejemplos  
 En la tabla siguiente se enumera los elementos protegibles y los temas que describen la sintaxis específica de los mismos.  
  
|||  
|-|-|  
|Rol de aplicación|[DENEGAR permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Ensamblado|[DENEGAR permisos de ensamblado &#40; Transact-SQL &#41;](../../t-sql/statements/deny-assembly-permissions-transact-sql.md)|  
|Clave asimétrica|[DENEGAR permisos de clave asimétrica &#40; Transact-SQL &#41;](../../t-sql/statements/deny-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidad|[DENEGAR permisos de grupo de disponibilidad &#40; Transact-SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)|  
|Certificado|[DENEGAR permisos de certificado &#40; Transact-SQL &#41;](../../t-sql/statements/deny-certificate-permissions-transact-sql.md)|  
|Contrato|[DENEGAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Base de datos|[DENEGAR permisos de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-permissions-transact-sql.md)|  
|Credencial con ámbito de base de datos|[DENEGAR el ámbito de base de datos de credencial (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)|  
|Extremo|[DENEGAR permisos de extremo &#40; Transact-SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)|  
|Catálogo de texto completo|[DENEGAR permisos de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|Lista de palabras irrelevantes de texto completo|[DENEGAR permisos de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|Función|[DENEGAR permisos de objetos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Inicio de sesión|[DENEGAR permisos de entidad de seguridad de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)|  
|Tipo de mensaje|[DENEGAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Object|[DENEGAR permisos de objetos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Cola|[DENEGAR permisos de objetos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Enlace de servicio remoto|[DENEGAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Rol|[DENEGAR permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Ruta|[DENEGAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|esquema|[DENEGAR permisos de esquema &#40; Transact-SQL &#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)|  
|Lista de propiedades de búsqueda|[DENEGAR permisos de lista de propiedades de búsqueda &#40; Transact-SQL &#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)|  
|Server|[DENEGAR permisos de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)|  
|ssNoVersion|[DENEGAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Procedimiento almacenado|[DENEGAR permisos de objetos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Clave simétrica|[DENEGAR permisos de clave simétrica &#40; Transact-SQL &#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)|  
|Synonym (Sinónimo)|[DENEGAR permisos de objetos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Objetos de sistema|[DENEGAR permisos de objeto de sistema &#40; Transact-SQL &#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)|  
|Tabla|[DENEGAR permisos de objetos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Tipo|[DENEGAR permisos de tipo de &#40; Transact-SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)|  
|Usuario|[DENEGAR permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Ver|[DENEGAR permisos de objetos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Colección de esquemas XML|[DENEGAR permisos de colección de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Vea también  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

