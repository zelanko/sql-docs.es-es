---
title: REVOKE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/26/2017
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
- REVOKE_TSQL
- REVOKE
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- REVOKE statement, Transact-SQL syntax
- removing permissions
- server-level securables [SQL Server]
- deleting permissions
- revoking permissions [SQL Server]
- REVOKE statement
- denying permissions [SQL Server], removing
- database-level securables [SQL Server]
- granting permissions [SQL Server], removing
- permissions [SQL Server], revoking
- dropping permissions
ms.assetid: 9d31d3e7-0883-45cd-bf0e-f0361bbb0956
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa08be63c0d792ed1e0422860b55a0c8f2abdc8b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-transact-sql"></a>REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita un permiso concedido o denegado previamente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for REVOKE  
REVOKE [ GRANT OPTION FOR ]  
      {   
        [ ALL [ PRIVILEGES ] ]  
        |  
                permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      }  
      [ ON [ class :: ] securable ]   
      { TO | FROM } principal [ ,...n ]   
      [ CASCADE] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
REVOKE   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    [ FROM | TO ] principal [ ,...n ]  
    [ CASCADE ]  
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
 GRANT OPTION FOR  
 Indica que se revocará la capacidad de conceder el permiso especificado. Se requiere cuando se utiliza el argumento CASCADE.  
  
> [!IMPORTANT]  
>  Si la entidad de seguridad dispone del permiso especificado sin la opción GRANT, se revocará el permiso.  
  
 ALL  
**Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Esta opción no revoca todos los permisos posibles. Revocar ALL es equivalente a revocar los siguientes permisos.  
  
-   Si el elemento protegible es una base de datos, ALL significa BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE y CREATE VIEW.  
  
-   Si el elemento protegible es una función escalar, ALL significa EXECUTE y REFERENCES.  
  
-   Si el elemento protegible es una función con valores de tabla, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
-   Si el elemento protegible es un procedimiento almacenado, ALL significa EXECUTE.  
  
-   Si el elemento protegible es una tabla, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
-   Si el elemento protegible es una vista, ALL significa DELETE, INSERT, REFERENCES, SELECT y UPDATE.  
  
> [!NOTE]  
>  La sintaxis de REVOKE ALL ha quedado desusada. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, revoque permisos concretos.  
  
 PRIVILEGES  
 Incluido por compatibilidad con ISO. No cambia el comportamiento de ALL.  
  
 *permiso*  
 Es el nombre de un permiso. Las asignaciones válidas de permisos para elementos protegibles se describen en los temas enumerados en [sintaxis específica del protegibles](#securable) más adelante en este tema.  
  
 *columna*  
 Especifica el nombre de una columna de una tabla en la que se van a revocar los permisos. Es obligatorio utilizar paréntesis.  
  
 *clase*  
 Especifica la clase del elemento protegible para el que se va a revocar el permiso. El calificador de ámbito **::** es necesario.  
  
 *elemento protegible*  
 Especifica el elemento protegible para el que se va a revocar el permiso.  
  
 PARA | DESDE *principal*  
 Es el nombre de una entidad de seguridad. Las entidades de seguridad de las que se pueden revocar permisos para un elemento protegible varían según el elemento. Para obtener más información acerca de las combinaciones válidas, vea los temas enumerados en [sintaxis específica del protegibles](#securable) más adelante en este tema.  
  
 CASCADE  
 Indica que el permiso que se va a revocar también se revocará de otras entidades de seguridad a la que se concedió a esta entidad de seguridad. Cuando se utiliza el argumento CASCADE, también se debe incluir el argumento GRANT OPTION FOR.  
  
> [!CAUTION]  
>  Una revocación en cascada de un permiso concedido WITH GRANT OPTION revocará tanto GRANT como DENY de dicho permiso.  
  
 AS *principal*  
 Use la cláusula AS principal para indicar que revocar un permiso que se ha concedido por una entidad de seguridad distintos que. Por ejemplo, suponga que el usuario Mary es principal_id 12 y usuario Raul es 15 principal. Mary y Raul concesión a que un usuario llamado a Carlos el mismo permiso. La tabla sys.database_permissions indicará los permisos dos veces, pero cada uno tendrá un valor de grantor_prinicpal_id diferentes. Mary pudo revocar el permiso utilizando la `AS RAUL` cláusula para quitar la concesión de Raul del permiso.
 
El uso de como en esta instrucción no implica la capacidad de suplantar a otro usuario.  
  
## <a name="remarks"></a>Comentarios  
 La sintaxis completa de la instrucción REVOKE es compleja. El diagrama de sintaxis anterior se ha simplificado para concentrar la atención en su estructura. La sintaxis completa para revocar los permisos en elementos protegibles específicos se describe en los temas enumerados en [sintaxis específica del protegibles](#securable) más adelante en este tema.  
  
 Se puede utilizar la instrucción REVOKE para retirar permisos concedidos y la instrucción DENY para evitar que una entidad de seguridad obtenga un permiso específico mediante una instrucción GRANT.  
  
 La concesión de un permiso quita DENY o REVOKE de ese permiso para el elemento protegible especificado. Si se deniega el mismo permiso en un ámbito superior que contiene el elemento protegible, DENY tiene prioridad. Sin embargo, revocar el permiso concedido en un ámbito superior no tienen prioridad.  
  
> [!CAUTION]  
>  Un permiso DENY de nivel de tabla no tiene prioridad sobre uno GRANT de nivel de columna. Se ha conservado esta incoherencia en la jerarquía de permisos para mantener la compatibilidad con versiones anteriores. Se quitará en una versión futura.  
  
 El procedimiento almacenado del sistema sp_helprotect informa de los permisos sobre un elemento protegible en el nivel de base de datos.  
  
 La instrucción REVOKE generará errores si no se especifica CASCADE al revocar un permiso de una entidad de seguridad que tenía concedido ese permiso con GRANT OPTION especificada.  
  
## <a name="permissions"></a>Permissions  
 Las entidades de seguridad con el permiso CONTROL para un elemento protegible pueden revocar permisos para ese elemento. Los propietarios de objetos pueden revocar permisos en los objetos que poseen.  
  
 Los receptores del permiso CONTROL SERVER, como los miembros del rol fijo de servidor sysadmin, pueden revocar los permisos en cualquier elemento protegible en el servidor. Los receptores del permiso CONTROL en una base de datos, como los miembros del rol fijo de base de datos db_owner, pueden revocar los permisos en cualquier elemento protegible en la base de datos. Los receptores del permiso CONTROL en un esquema pueden revocar los permisos en cualquier objeto del esquema.  
  
##  <a name="securable"></a>Sintaxis específica del elemento protegible  
 En la tabla siguiente se enumera los elementos protegibles y los temas que describen la sintaxis específica de los mismos.  
  
|Elemento protegible|Tema|  
|---------------|-----------|  
|Rol de aplicación|[REVOCAR permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Ensamblado|[REVOCAR permisos de ensamblado &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-assembly-permissions-transact-sql.md)|  
|Clave asimétrica|[REVOCAR permisos de clave asimétrica &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidad|[Permisos de grupo de disponibilidad REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)|  
|Certificado|[REVOCAR permisos de certificado &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-certificate-permissions-transact-sql.md)|  
|Contrato|[REVOCAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Base de datos|[REVOCAR permisos de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-permissions-transact-sql.md)|  
|Extremo|[REVOCAR permisos de extremo &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)|  
|Credencial con ámbito de base de datos|[Ámbito de base de datos de revocación credencial (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)|  
|Catálogo de texto completo|[REVOCAR permisos de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|Lista de palabras irrelevantes de texto completo|[REVOCAR permisos de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|Función|[REVOCAR permisos de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Inicio de sesión|[REVOCAR permisos de entidad de seguridad de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)|  
|Tipo de mensaje|[REVOCAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Object|[REVOCAR permisos de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Cola|[REVOCAR permisos de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Enlace de servicio remoto|[REVOCAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Rol|[REVOCAR permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Ruta|[REVOCAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|esquema|[REVOCAR permisos de esquema &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-schema-permissions-transact-sql.md)|  
|Lista de propiedades de búsqueda|[REVOCAR permisos de lista de propiedades de búsqueda &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-search-property-list-permissions-transact-sql.md)|  
|Server|[REVOCAR permisos de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)|  
|ssNoVersion|[REVOCAR permisos de Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Procedimiento almacenado|[REVOCAR permisos de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Clave simétrica|[REVOCAR permisos de clave simétrica &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)|  
|Synonym (Sinónimo)|[REVOCAR permisos de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Objetos de sistema|[REVOCAR permisos de objeto de sistema &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)|  
|Tabla|[REVOCAR permisos de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Tipo|[REVOCAR permisos de tipo de &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)|  
|Usuario|[REVOCAR permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Ver|[REVOCAR permisos de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Colección de esquemas XML|[REVOCAR permisos de colección de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía de permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

