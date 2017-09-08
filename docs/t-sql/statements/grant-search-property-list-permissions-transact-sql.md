---
title: "Permisos de lista de propiedades de búsqueda de GRANT (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], permissions
- search property lists [SQL Server], permissions
- granting permissions [SQL Server], search property lists
- GRANT statement, search property list permissions
ms.assetid: bb2d2550-9c0e-4a88-b50c-12e481d4d3ae
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f004c02e0461eeeffadf3b30bae90426e081faef
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-search-property-list-permissions-transact-sql"></a>Conceder permisos de lista de propiedades de búsqueda (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Concede los permisos en una lista de propiedades de búsqueda.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GRANT permission [ ,...n ] ON   
    SEARCH PROPERTY LIST :: search_property_list_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permiso*  
 Es el nombre de un permiso. Las asignaciones válidas de permisos a elementos protegibles se describen en la sección "Comentarios", más adelante en este tema.  
  
 EN la lista de propiedades de búsqueda **::***search_property_list_name*  
 Especifica la lista de propiedades de búsqueda para la que se concede el permiso. El calificador de ámbito **::** es necesario.  
  
 **Para ver las propiedades de búsqueda existentes listas**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 *database_principal*  
 Especifica la entidad de seguridad para la que se concede el permiso. La entidad de seguridad puede ser un:  
  
-   usuario de base de datos  
  
-   rol de base de datos  
  
-   rol de aplicación  
  
-   usuario de base de datos asignado a un inicio de sesión de Windows  
  
-   usuario de base de datos asignado a un grupo de Windows  
  
-   usuario de base de datos asignado a un certificado  
  
-   usuario de base de datos asignado a una clave asimétrica  
  
-   usuario de base de datos no asignado a una entidad de seguridad del servidor  
  
 GRANT OPTION  
 Indica que la entidad de seguridad también podrá conceder el permiso especificado a otras entidades de seguridad.  
  
 AS *granting_principal*  
 Especifica una entidad de seguridad de la que la entidad de seguridad que ejecuta esta consulta deriva su derecho de conceder el permiso. La entidad de seguridad puede ser un:  
  
-   usuario de base de datos  
  
-   rol de base de datos  
  
-   rol de aplicación  
  
-   usuario de base de datos asignado a un inicio de sesión de Windows  
  
-   usuario de base de datos asignado a un grupo de Windows  
  
-   usuario de base de datos asignado a un certificado  
  
-   usuario de base de datos asignado a una clave asimétrica  
  
-   usuario de base de datos no asignado a una entidad de seguridad del servidor  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="search-property-list-permissions"></a>Permisos de lista de propiedades de búsqueda  
 Una lista de propiedades de búsqueda es un elemento protegible de nivel de base de datos que contiene la base de datos que es su entidad primaria en la jerarquía de permisos. Los permisos más limitados y específicos que se pueden conceder en una lista de propiedades de búsqueda se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de lista de propiedades de búsqueda|Implícito en el permiso de lista de propiedades de búsqueda|Implícito en el permiso de base de datos|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 El otorgante del permiso (o la entidad de seguridad especificada con la opción AS) debe tener el permiso con GRANT OPTION, o un permiso superior que implique el permiso que se va a conceder.  
  
 Si utiliza la opción AS, se aplican los siguientes requisitos adicionales.  
  
|AS *granting_principal*|Permiso adicional necesario|  
|------------------------------|------------------------------------|  
|Usuario de la base de datos|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un inicio de sesión de Windows|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un grupo de Windows|Pertenencia al grupo de Windows, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un certificado|Pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a una clave asimétrica|Pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos no asignado a una entidad de seguridad del servidor|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Rol de base de datos|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Rol de aplicación|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
  
 Los propietarios de objetos pueden conceder permisos para los objetos que poseen. Las entidades de seguridad con permiso CONTROL sobre un elemento protegible pueden conceder permisos para ese elemento.  
  
 Los receptores del permiso CONTROL SERVER como los miembros del rol fijo de servidor sysadmin pueden conceder los permisos sobre cualquier elemento protegible en el servidor. Los receptores del permiso CONTROL para una base de datos, como los miembros del rol fijo de base de datos db_owner, pueden conceder los permisos para cualquier elemento protegible en la base de datos. Los receptores del permiso CONTROL en un esquema pueden conceder los permisos en cualquier objeto del esquema.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="granting-permissions-to-a-search-property-list"></a>Conceder permisos a una lista de propiedades de búsqueda  
 En el ejemplo siguiente, se concede a `Mary` el permiso `VIEW DEFINITION` en la lista de propiedades de búsqueda `DocumentTablePropertyList`.  
  
```  
GRANT VIEW DEFINITION  
    ON SEARCH PROPERTY LIST :: DocumentTablePropertyList  
    TO Mary ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear rol de aplicación &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [Crear lista de propiedades de búsqueda &#40; Transact-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [DENEGAR permisos de lista de propiedades de búsqueda &#40; Transact-SQL &#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Sys.fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOCAR permisos de lista de propiedades de búsqueda &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-search-property-list-permissions-transact-sql.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Sys.registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  

