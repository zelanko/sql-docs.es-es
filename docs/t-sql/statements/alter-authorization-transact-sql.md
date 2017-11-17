---
title: ALTER AUTHORIZATION (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/07/2017
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
- ALTER_AUTHORIZATION_TSQL
- ALTER AUTHORIZATION
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], transferring
- modifying entity ownership
- full-text search [SQL Server], permissions
- owners [SQL Server], entities
- ALTER AUTHORIZATION statement
- entity ownership [SQL Server]
- transferring ownership
- search property lists [SQL Server], permissions
- TAKE OWNERSHIP
ms.assetid: 8c805ae2-91ed-4133-96f6-9835c908f373
caps.latest.revision: 84
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31738dcb4eaf4676b4c0a34b13ee400e89333428
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-authorization-transact-sql"></a>ALTER AUTHORIZATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cambia la propiedad de un elemento protegible.    
    
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxis    
    
```    
-- Syntax for SQL Server  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
        OBJECT | ASSEMBLY | ASYMMETRIC KEY | AVAILABILITY GROUP | CERTIFICATE     
      | CONTRACT | TYPE | DATABASE | ENDPOINT | FULLTEXT CATALOG     
      | FULLTEXT STOPLIST | MESSAGE TYPE | REMOTE SERVICE BINDING    
      | ROLE | ROUTE | SCHEMA | SEARCH PROPERTY LIST | SERVER ROLE     
      | SERVICE | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

```
-- Syntax for SQL Database  
  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
      OBJECT | ASSEMBLY | ASYMMETRIC KEY | CERTIFICATE     
    | TYPE | DATABASE | FULLTEXT CATALOG     
    | FULLTEXT STOPLIST     
    | ROLE | SCHEMA | SEARCH PROPERTY LIST     
    | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

    
```    
-- Syntax for Azure SQL Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
```    
-- Syntax for Parallel Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      DATABASE     
    | SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      database_name 
    | schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
## <a name="arguments"></a>Argumentos    
\<class_type > es la clase protegible de la entidad para el que se va a cambiar el propietario. El valor predeterminado es OBJECT.    
    
|||    
|-|-|    
|OBJECT|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], almacenamiento de datos SQL Azure, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].|    
|ASSEMBLY|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|ASYMMETRIC KEY|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|AVAILABILITY GROUP |**Se aplica**: SQL Server 2012 a través [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|
|CERTIFICATE|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|CONTRACT|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|DATABASE|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Para obtener más información, consulte [ALTER autorización para bases de datos](#AlterDB) sección más adelante.|    
|ENDPOINT|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|FULLTEXT CATALOG|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|FULLTEXT STOPLIST|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|MESSAGE TYPE|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|REMOTE SERVICE BINDING|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|ROLE|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|ROUTE|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|SCHEMA|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], almacenamiento de datos SQL Azure, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].|    
|SEARCH PROPERTY LIST|**Se aplica**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|SERVER ROLE|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|SERVICE|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|SYMMETRIC KEY|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|TYPE|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|XML SCHEMA COLLECTION|**Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
    
 *nombre_de_entidad*    
 Es el nombre de la entidad.    
    
 *principal_name* | PROPIETARIO DEL ESQUEMA    
 Nombre de la entidad de seguridad que va a ser propietaria de la entidad. Los objetos de base de datos deben tener una entidad de base de datos como propietaria; un usuario o rol de base de datos. Los objetos de servidor (como bases de datos) deben tener una entidad de servidor (un inicio de sesión) como propietaria. Especifique **propietario del esquema** como el *principal_name* para indicar que el objeto debería pertenecer la entidad que posee el esquema del objeto.    
    
## <a name="remarks"></a>Comentarios    
 Se puede usar ALTER AUTHORIZATION para cambiar la propiedad de cualquier entidad que tenga propietario. La propiedad de las entidades que contienen bases de datos se puede transferir a cualquier entidad de seguridad de nivel de base de datos. La propiedad de las entidades de nivel de servidor solo se puede transferir a entidades de seguridad de nivel de servidor.    
    
> [!IMPORTANT]    
>  A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], un usuario puede ser propietario de un objeto o un tipo contenido en un esquema de otro usuario de la base de datos. Es un cambio de comportamiento con respecto a versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [OBJECTPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/objectproperty-transact-sql.md) y [TYPEPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/typeproperty-transact-sql.md).    
    
 Se puede transferir la propiedad de las siguientes entidades contenidas en esquemas de tipo "objeto": tablas, vistas, funciones, procedimientos, colas y sinónimos.    
    
 No se puede transferir la propiedad de las siguientes entidades: servidores vinculados, estadísticas, restricciones, reglas, valores predeterminados, desencadenadores, colas de [!INCLUDE[ssSB](../../includes/sssb-md.md)], credenciales, funciones de partición, esquemas de partición, claves maestras de bases de datos, clave maestra de servicios y notificaciones de eventos.    
    
 No se puede transferir la propiedad de los miembros de las siguientes clases de elementos protegibles: servidor, inicio de sesión, usuario, rol de aplicación y columna.    
    
 La opción SCHEMA OWNER solo es válida cuando se transfiere la propiedad de una entidad que contiene esquemas. SCHEMA OWNER transferirá la propiedad de la entidad al propietario del esquema en el que reside. Solo las entidades de clase OBJECT, TYPE o XML SCHEMA COLLECTION contienen esquemas.    
    
 Si la entidad de destino no es una base de datos y la entidad se va a transferir a un nuevo propietario, se quitarán todos los permisos del destino.    
    
> [!CAUTION]    
>  En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], el comportamiento de los esquemas es distinto del de las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si en el código se supone que los esquemas son equivalentes a usuarios de base de datos, los resultados obtenidos podrían ser incorrectos. Las vistas de catálogo antiguas, incluida sysobjects, no deben usarse en una base de datos en la que se haya usado alguna de las siguientes instrucciones DDL: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. En una base de datos en la que se ha usado alguna de estas instrucciones, deben usarse las nuevas vistas de catálogo. En las nuevas vistas de catálogo se tiene en cuenta la separación de entidades de seguridad y esquemas que se presentó en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obtener más información sobre las vistas de catálogo, vea [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).    
    
 Tenga en cuenta los siguientes aspectos:    
    
> [!IMPORTANT]    
>  Es la única manera confiable de localizar al propietario de un objeto de consulta el **sys.objects** vista de catálogo. La única manera confiable de localizar al propietario de un tipo consiste en utilizar la función TYPEPROPERTY.    
    
## <a name="special-cases-and-conditions"></a>Condiciones y casos especiales    
 En la siguiente tabla se enumeran los casos especiales, las excepciones y las condiciones que se aplican para modificar la autorización.    
    
|Clase|Condición|    
|-----------|---------------|    
|OBJECT|No se puede cambiar la propiedad de desencadenadores, restricciones, reglas, valores predeterminados, estadísticas, objetos del sistema, colas, vistas indizadas o tablas con vistas indizadas.|    
|SCHEMA|Cuando se transfiere la propiedad, se quitarán los permisos en objetos contenidos en esquemas que no tengan propietarios explícitos. No se puede cambiar el propietario de sys, dbo o information_schema.|    
|TYPE|No se puede cambiar la propiedad de un TYPE que pertenece a sys o information_schema.|    
|CONTRACT, MESSAGE TYPE o SERVICE|No se puede cambiar la propiedad de entidades del sistema.|    
|SYMMETRIC KEY|No se puede cambiar la propiedad de claves globales temporales.|    
|CERTIFICATE o ASYMMETRIC KEY|No se puede transferir la propiedad de estas entidades a un rol o un grupo.|    
|ENDPOINT|La entidad de seguridad debe ser un inicio de sesión.|    
  
## <a name="AlterDB"></a>ALTER AUTHORIZATION para bases de datos  
**SE APLICA**: [!INCLUDE[ssSQL15](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
### <a name="for-sql-server"></a>Para SQL Server:  
**Requisitos para el nuevo propietario:**   
La nueva entidad de seguridad de propietario debe ser uno de los siguientes:  
-   Un inicio de sesión de autenticación de SQL Server.  
-   Un inicio de sesión de autenticación de Windows que representa un usuario de Windows (no un grupo).  
-   Un usuario de Windows que autentica a través de un inicio de sesión de autenticación de Windows que representa un grupo de Windows.  
  
**Requisitos para la persona que ejecuta la instrucción ALTER AUTHORIZATION:**  
Si no es un miembro de la **sysadmin** rol fijo de servidor, debe tener al menos TAKE OWNERSHIP en la base de datos y debe tener el permiso IMPERSONATE en el nuevo inicio de sesión del propietario.   

### <a name="for-azure-sql-database"></a>Base de datos de SQL Azure:  
**Requisitos para el nuevo propietario:**   
La nueva entidad de seguridad de propietario debe ser uno de los siguientes:  
-   Un inicio de sesión de autenticación de SQL Server.  
-   Un usuario federado (no un grupo) presente en Azure AD.  
-   Un usuario administrado (no un grupo) o una aplicación en Azure AD.    

> [!NOTE]  
> Si el nuevo propietario es un usuario de Azure Active Directory, no puede existir como un usuario en la base de datos donde el nuevo propietario se convertirá en el DBO nuevo. Estos usuarios de Azure AD deben quitarse primero desde la base de datos antes de ejecutar la instrucción ALTER AUTHORIZATION cambiar la propiedad de base de datos al nuevo usuario. Para obtener más información acerca de cómo configurar un usuarios de Azure Active Directory con la base de datos SQL, consulte [conectarse a la base de datos SQL o SQL datos almacenamiento mediante Azure Active Directory autenticación](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
**Requisitos para la persona que ejecuta la instrucción ALTER AUTHORIZATION:**  
Debe conectarse a la base de datos de destino para cambiar el propietario de esa base de datos.  

Los siguientes tipos de cuentas pueden cambiar el propietario de una base de datos. 
* El inicio de sesión de entidad de seguridad de nivel de servicio. (El Administrador de SQL Azure proporcionado cuando se creó el servidor lógico.)  
* El Administrador de Azure Active Directory para el servidor de SQL Azure.   
* El propietario actual de la base de datos.   
 
  
En la tabla siguiente se resume los requisitos:  
  
Ejecutor  |Destino  |Resultado    
---------|---------|---------  
Inicio de sesión de autenticación de SQL Server     |Inicio de sesión de autenticación de SQL Server         |Success  
Inicio de sesión de autenticación de SQL Server     |Usuario de Azure AD         |Un error           
Usuario de Azure AD     |Inicio de sesión de autenticación de SQL Server         |Success           
Usuario de Azure AD     |Usuario de Azure AD         |Success           
  
Para comprobar un propietario de Azure AD de la base de datos ejecute el siguiente comando de Transact-SQL en una base de datos de usuario (en este ejemplo `testdb`).  
    
```    
SELECT CAST(owner_sid as uniqueidentifier) AS Owner_SID   
FROM sys.databases   
WHERE name = 'testdb';  
```    
    
El resultado será un identificador (por ejemplo, 6D8B81F6-7C79-444C-8858-4AF896C03C67) que se corresponde con Azure AD ObjectID asignado a`richel@cqclinic.onmicrosoft.com`  
Cuando un usuario de inicio de sesión de autenticación de SQL Server es el propietario de la base de datos, ejecute la instrucción siguiente en la base de datos maestra para comprobar el propietario de la base de datos:  
    
```    
SELECT d.name, d.owner_sid, sl.name   
FROM sys.databases AS d  
JOIN sys.sql_logins AS sl  
ON d.owner_sid = sl.sid;  
    
```    
  
### <a name="best-practice"></a>Práctica recomendada  
  
En lugar de usuarios de Azure AD como propietarios individuales de la base de datos, utilice un grupo de Azure AD como un miembro de la **db_owner** rol fijo de base de datos. Los pasos siguientes, se muestra cómo configurar un inicio de sesión deshabilitado como propietario de la base de datos y hacer que un grupo de Active Directory de Azure (`mydbogroup`) un miembro de la **db_owner** rol. 
1.  Inicie sesión en SQL Server como administrador de Azure AD y cambiar el propietario de la base de datos a un inicio de sesión de autenticación de SQL Server deshabilitado. Por ejemplo, desde la base de datos de usuario ejecute:  
  ```    
  ALTER AUTHORIZATION ON database::testdb TO DisabledLogin;  
  ```    
2.  Crear un grupo de Azure AD debe poseer la base de datos y agregarlo como un usuario a la base de datos de usuario. Por ejemplo:  
  ```    
  CREATE USER [mydbogroup] FROM EXTERNAL PROVIDER;  
  ```    
3.  En la base de datos de usuario, agregue el usuario que representa el grupo de Azure AD, en la **db_owner** rol fijo de base de datos. Por ejemplo:  
  ```    
  ALTER ROLE db_owner ADD MEMBER mydbogroup;  
  ```    
  
Ahora el `mydbogroup` los miembros pueden administrar centralmente la base de datos como miembros de la **db_owner** rol.  
- Cuando los miembros de este grupo se quitarán del grupo de Azure AD, automáticamente pierdan los permisos dbo para esta base de datos.  
- De forma similar si se agregan nuevos miembros a `mydbogroup` grupo de Azure AD, que obtengan automáticamente el acceso de dbo para esta base de datos.  
  
Para comprobar si un usuario específico tiene el permiso efectivo dbo, hacer que el usuario ejecute la instrucción siguiente:  
    
```    
SELECT IS_MEMBER ('db_owner');  
```    
  
Un valor devuelto de 1 indica que el usuario es un miembro del rol.  
   
    
## <a name="permissions"></a>Permissions    
 Requiere el permiso TAKE OWNERSHIP en la entidad. Si el propietario no es el usuario que ejecuta esta instrucción, también se necesita, 1) el permiso IMPERSONATE en el nuevo propietario si es un usuario o inicio de sesión; o 2) si el nuevo propietario es un rol, debe pertenecer al rol, o el permiso ALTER en el rol; o 3) si el nuevo propietario es un rol de aplicación, el permiso ALTER en el rol de aplicación.    
    
## <a name="examples"></a>Ejemplos    
    
### <a name="a-transfer-ownership-of-a-table"></a>A. Transferir la propiedad de una tabla    
 En el siguiente ejemplo se transfiere la propiedad de la tabla `Sprockets` al usuario `MichikoOsada`. La tabla se encuentra dentro del esquema `Parts`.    
    
```    
ALTER AUTHORIZATION ON OBJECT::Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
 La consulta también podría ser similar a la siguiente:    
    
```    
ALTER AUTHORIZATION ON Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
 Si el esquema de objetos no se incluye como parte de la instrucción, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] tendrá un aspecto para el objeto en el esquema predeterminado de los usuarios. Por ejemplo:    
    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
```    
    
### <a name="b-transfer-ownership-of-a-view-to-the-schema-owner"></a>B. Transferir la propiedad de una vista al propietario del esquema    
 En el siguiente ejemplo se transfiere la propiedad de la vista `ProductionView06` al propietario del esquema que la contiene. La vista se encuentra dentro del esquema `Production`.    
    
```    
ALTER AUTHORIZATION ON OBJECT::Production.ProductionView06 TO SCHEMA OWNER;    
GO    
```    
    
### <a name="c-transfer-ownership-of-a-schema-to-a-user"></a>C. Transferir la propiedad de un esquema a un usuario    
 En el siguiente ejemplo se transfiere la propiedad del esquema `SeattleProduction11` al usuario `SandraAlayo`.    
    
```    
ALTER AUTHORIZATION ON SCHEMA::SeattleProduction11 TO SandraAlayo;    
GO    
```    
    
### <a name="d-transfer-ownership-of-an-endpoint-to-a-sql-server-login"></a>D. Transferir la propiedad de un extremo a un inicio de sesión de SQL Server    
 En el siguiente ejemplo se transfiere la propiedad del extremo `CantabSalesServer1` a `JaePak`. Puesto que el extremo es un elemento protegible de nivel de servidor, el extremo solo puede transferirse a una entidad de seguridad de nivel de servidor.    
    
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].    
    
```    
ALTER AUTHORIZATION ON ENDPOINT::CantabSalesServer1 TO JaePak;    
GO    
```    
    
### <a name="e-changing-the-owner-of-a-table"></a>E. Cambiar el propietario de una tabla    
 Cada uno de los ejemplos siguientes cambia el propietario de la `Sprockets` tabla el `Parts` base de datos para el usuario de base de datos `MichikoOsada`.    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON dbo.Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::dbo.Sprockets TO MichikoOsada;    
```    
    
### <a name="f-changing-the-owner-of-a-database"></a>F. Cambiar el propietario de una base de datos    
 **Se aplica**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].    
    
 En el ejemplo siguiente se cambia el propietario de la `Parts` base de datos para el inicio de sesión `MichikoOsada`.    
    
```    
ALTER AUTHORIZATION ON DATABASE::Parts TO MichikoOsada;    
```    
  
### <a name="g-changing-the-owner-of-a-sql-database-to-an-azure-ad-user"></a>G. Cambiar el propietario de una base de datos de SQL a un usuario de AD de Azure  
En el ejemplo siguiente, un administrador de Azure Active Directory para SQL Server en una organización con un active directory denominado `cqclinic.onmicrosoft.com`, puede cambiar la propiedad actual de una base de datos `targetDB` y realizar un usuario AAD `richel@cqclinic.onmicorsoft.com` la nueva base de datos propietario con el comando siguiente:  
    
```    
ALTER AUTHORIZATION ON database::targetDB TO [rachel@cqclinic.onmicrosoft.com];   
```    
    
 Tenga en cuenta que, para usuarios de Azure AD se deben utilizar los corchetes que encierran el nombre de usuario.  
  
    
## <a name="see-also"></a>Vea también    
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)     
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)     
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)    
 

