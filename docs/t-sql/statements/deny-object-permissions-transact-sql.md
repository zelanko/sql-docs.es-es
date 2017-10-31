---
title: DENEGAR permisos de objeto (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
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
- DENY statement, objects
- table permissions [SQL Server]
ms.assetid: 0b8d3ddc-38c0-4241-b7bb-ee654a5081aa
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2655a796d6d097cb635576313664ea6bfa7162db
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="deny-object-permissions-transact-sql"></a>DENY (permisos de objeto de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Deniega permisos para un miembro de la clase OBJECT de elementos protegibles. Éstos son los miembros de la clase OBJECT: tablas, vistas, funciones con valores de tabla, procedimientos almacenados, procedimientos almacenados extendidos, funciones escalares, funciones de agregado, colas de servicio y sinónimos.  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DENY <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
        TO <database_principal> [ ,...n ]   
    [ CASCADE ]  
        [ AS <database_principal> ]  
  
<permission> ::=  
    ALL [ PRIVILEGES ] | permission [ ( column [ ,...n ] ) ]  
  
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
 Especifica un permiso que se puede denegar en un objeto contenido en un esquema. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 ALL  
 Si deniega ALL no se deniegan todos los permisos posibles. Denegar ALL es equivalente a denegar todos los permisos ANSI-92 aplicables al objeto especificado. El significado de ALL varía de la siguiente forma:  
  
 - Permisos de función escalar: EXECUTE, REFERENCES.  
 - Permisos de función con valores de tabla: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
 - Permisos de procedimientos almacenados: ejecución.  
 - Permisos de tabla: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
 - Permisos de vista: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
PRIVILEGES  
 Incluido para la compatibilidad con ANSI-92. No cambia el comportamiento de ALL.  
  
*columna*  
 Especifica el nombre de una columna de una tabla, vista o función con valores de tabla para la que se deniega el permiso. Los paréntesis **()** son necesarios. Solo es posible denegar los permisos SELECT, REFERENCES y UPDATE para una columna. *columna* se pueden especificar en la cláusula de permisos o después del nombre del elemento protegible.  
  
> [!CAUTION]  
>  Un permiso DENY de nivel de tabla no tiene prioridad sobre uno GRANT de nivel de columna. Se ha conservado esta incoherencia en la jerarquía de permisos para mantener la compatibilidad con versiones anteriores.  
  
 ON [objeto **::** ] [ *schema_name* ] **.** *object_name*  
 Especifica el objeto en el que se va a denegar el permiso. La frase OBJECT es opcional si *schema_name* se especifica. Si se utiliza la frase OBJECT, el calificador de ámbito (**::**) es necesario. Si *schema_name* no se especifica, se utiliza el esquema predeterminado. Si *schema_name* se especifica, el calificador de ámbito de esquema (**.**) es necesario.  
  
 PARA \<database_principal >  
 Especifica la entidad de seguridad a la que se deniega el permiso.  
  
 CASCADE  
 Indica que el permiso que se va a denegar también se denegará a otras entidades de seguridad a las que esta entidad de seguridad ha concedido permisos.  
  
 AS \<database_principal >  
 Especifica una entidad de seguridad de la que la entidad de seguridad que ejecuta esta consulta deriva su derecho de denegar el permiso.  
  
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
 Puede ver la información acerca de objetos en varias vistas de catálogo. Para obtener más información, vea [vistas de catálogo de objetos &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 Un objeto es un elemento protegible de nivel de esquema que contiene el esquema que es su entidad primaria en la jerarquía de permisos. La mayoría de permisos limitados y específicos que se pueden denegar en un objeto se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de objeto|Implícito en el permiso de objeto|Implícito en el permiso del esquema|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|DELETE|CONTROL|DELETE|  
|Ejecute|CONTROL|Ejecute|  
|INSERT|CONTROL|INSERT|  
|RECEIVE|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|RECEIVE|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|VIEW CHANGE TRACKING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL en el objeto.  
  
 Si utiliza la cláusula AS, la entidad de seguridad especificada debe ser propietaria del objeto en el que se deniegan los permisos.  
  
## <a name="examples"></a>Ejemplos  
Los ejemplos siguientes usan la base de datos de AdventureWorks.
  
### <a name="a-denying-select-permission-on-a-table"></a>A. Denegar el permiso SELECT en una tabla  
 El siguiente ejemplo se deniega `SELECT` permiso al usuario `RosaQdM` en la tabla `Person.Address`.  
  
```  
DENY SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-denying-execute-permission-on-a-stored-procedure"></a>B. Denegar el permiso EXECUTE en un procedimiento almacenado  
 En el siguiente ejemplo se deniega el permiso `EXECUTE` para el procedimiento almacenado `HumanResources.uspUpdateEmployeeHireInfo` a un rol de aplicación denominado `Recruiting11`.  
  
```  
DENY EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-denying-references-permission-on-a-view-with-cascade"></a>C. Denegar el permiso REFERENCES en una vista con CASCADE  
 En el siguiente ejemplo se deniega el permiso `REFERENCES` para la columna `BusinessEntityID` de la vista `HumanResources.vEmployee` al usuario `Wanida` con `CASCADE`.  
  
```  
DENY REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Permisos de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [REVOCAR permisos de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [Sys.fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  

