---
title: "Permisos de colección de esquemas XML de la instrucción GRANT (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
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
- GRANT statement, XML schema collections
- XML schema collections [SQL Server], permissions
- granting permissions [SQL Server], XML schema collections
- schema collections [SQL Server], permissions
ms.assetid: 57e24465-cd43-45cf-bb52-eea0b49867f9
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae2fdb5dfbeb648264f8d9fe7cfc5dac977bd57d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-xml-schema-collection-permissions-transact-sql"></a>GRANT (permisos de colección de esquemas XML de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permisos para una colección de esquemas XML.   
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GRANT permission  [ ,...n ] ON   
    XML SCHEMA COLLECTION :: [ schema_name . ]  
    XML_schema_collection_name  
    TO <database_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS <database_principal> ]   
  
<database_principal> ::=   
        Database_user   
    | Database_role   
    | Application_role   
    | Database_user_mapped_to_Windows_User   
    | Database_user_mapped_to_Windows_Group   
    | Database_user_mapped_to_certificate   
    | Database_user_mapped_to_asymmetric_key   
    | Database_user_with_no_login  
```  
  
## <a name="arguments"></a>Argumentos  
 *permiso*  
 Especifica un permiso que se puede conceder para una colección de esquemas XML. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 COLECCIÓN de esquemas XML ON:: [ *schema_name*. ] *XML_schema_collection_name*  
 Especifica la colección de esquemas XML en la que se va a conceder el permiso. Se requiere el calificador de ámbito (::). Si *schema_name* no se especifica, se utilizará el esquema predeterminado. Si *schema_name* se especifica, se requiere el calificador de ámbito de esquema (.).  
  
 \<database_principal > especifica la entidad a la que se va a conceder el permiso.  
  
 WITH GRANT OPTION  
 Indica que la entidad de seguridad también podrá conceder el permiso especificado a otras entidades de seguridad.  
  
 AS \<database_principal > especifica una entidad de seguridad de la que la entidad de seguridad para ejecutar esta consulta deriva su derecho a conceder el permiso.  
  
 *Database_user*  
 Especifica un usuario de base de datos.  
  
 *Database_role*  
 Especifica un rol de base de datos.  
  
 *Application_role*  
 Especifica un rol de aplicación.  
  
 *Database_user_mapped_to_Windows_User*  
 Especifica un usuario de base de datos asignado a un usuario de Windows.  
  
 *Database_user_mapped_to_Windows_Group*  
 Especifica un usuario de base de datos asignado a un grupo de Windows.  
  
 *Database_user_mapped_to_certificate*  
 Especifica un usuario de base de datos asignado a un certificado.  
  
 *Database_user_mapped_to_asymmetric_key*  
 Especifica un usuario de base de datos asignado a una clave asimétrica.  
  
 *Database_user_with_no_login*  
 Especifica un usuario de base de datos sin entidad de seguridad de servidor correspondiente.  
  
## <a name="remarks"></a>Comentarios  
 Información sobre las colecciones de esquemas XML está visible en el [sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md) vista de catálogo.  
  
 Una colección de esquemas XML es un elemento protegible de nivel de esquema que contiene el esquema que es su entidad primaria en la jerarquía de permisos. La mayoría de los permisos limitados y específicos que se pueden conceder para una colección de esquemas XML se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de colección de esquemas XML|Implicado por el permiso de colección de esquemas XML|Implícito en el permiso del esquema|  
|--------------------------------------|-------------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|Ejecute|CONTROL|Ejecute|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 El otorgante del permiso (o la entidad de seguridad especificada con la opción AS) debe tener el permiso con GRANT OPTION, o un permiso superior que implique el permiso que se va a conceder.  
  
 Si utiliza la opción AS, se aplican los siguientes requisitos adicionales.  
  
|AS|Permiso adicional necesario|  
|--------|------------------------------------|  
|Usuario de la base de datos|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un inicio de sesión de Windows|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un grupo de Windows|Pertenencia al grupo de Windows, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un certificado|Pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a una clave asimétrica|Pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos no asignado a una entidad de seguridad del servidor|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Rol de base de datos|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Rol de aplicación|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se concede el permiso `EXECUTE` para la colección de esquemas XML `Invoices4` al usuario `Wanida`. La colección de esquemas XML `Invoices4` se ubica dentro del esquema `Sales` de la base de datos `AdventureWorks2012`.  
  
 ```
 USE AdventureWorks2012;  
 GRANT EXECUTE ON XML SCHEMA COLLECTION::Sales.Invoices4 TO Wanida;  
 GO
 ```  
  
## <a name="see-also"></a>Vea también  
 [DENEGAR permisos de colección de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)   
 [REVOCAR permisos de colección de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)   
 [Sys.xml_schema_collections &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md)   
 [Crear colección de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


