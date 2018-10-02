---
title: DENY (permisos de esquema de Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [SQL Server], schemas
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
- DENY statement, schemas
ms.assetid: 300a67c4-d226-4653-9e9f-7ae4d53fcf33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 10812df142aa71329df5d5b024d3a18d5216e250
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701023"
---
# <a name="deny-schema-permissions-transact-sql"></a>DENY (permisos de esquema de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Deniega permisos en un esquema.  
  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DENY permission  [ ,...n ] } ON SCHEMA :: schema_name  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica un permiso que se puede denegar en un esquema. Para obtener una lista de estos permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 ON SCHEMA **::** schema *_name*  
 Especifica el esquema en el que se va a denegar el permiso. El calificador de ámbito **::** es obligatorio.  
  
 *database_principal*  
 Especifica la entidad de seguridad a la que se deniega el permiso. *database_principal* puede ser uno de los valores siguientes:  
  
-   Usuario de la base de datos  
-   Rol de base de datos  
-   Rol de aplicación  
-   Usuario de la base de datos asignado a un inicio de sesión de Windows  
-   Usuario de la base de datos asignado a un grupo de Windows  
-   Usuario de la base de datos asignado a un certificado  
-   Usuario de la base de datos asignado a una clave asimétrica  
-   Usuario de la base de datos no asignado a una entidad de seguridad de servidor  
  
CASCADE  
 Indica que el permiso que se va a denegar también se denegará a otras entidades de seguridad a las que esta entidad de seguridad ha concedido permisos.  
  
*denying_principal*  
 Especifica una entidad de seguridad de la que la entidad de seguridad que ejecuta esta consulta deriva su derecho de denegar el permiso. *denying_principal* puede ser uno de los valores siguientes:  
  
-   Usuario de la base de datos  
-   Rol de base de datos  
-   Rol de aplicación  
-   Usuario de la base de datos asignado a un inicio de sesión de Windows  
-   Usuario de la base de datos asignado a un grupo de Windows  
-   Usuario de la base de datos asignado a un certificado  
-   Usuario de la base de datos asignado a una clave asimétrica  
-   Usuario de la base de datos no asignado a una entidad de seguridad de servidor  
  
## <a name="remarks"></a>Notas  
 Un esquema es un elemento protegible de nivel de base de datos incluido en la base de datos que es su entidad primaria en la jerarquía de permisos. Los permisos más específicos y limitados que se pueden denegar en un esquema se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso del esquema|Implícito en el permiso del esquema|Implícito en el permiso de base de datos|  
|-----------------------|----------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SCHEMA|  
|CONTROL|CONTROL|CONTROL|  
|CREATE SEQUENCE|ALTER|ALTER ANY SCHEMA|  
|Delete|CONTROL|Delete|  
|Ejecute|CONTROL|Ejecute|  
|INSERT|CONTROL|INSERT|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|CONTROL|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL en el esquema. Si utiliza la opción AS, la entidad de seguridad especificada debe ser propietaria del esquema.  
  
## <a name="see-also"></a>Ver también  
 [CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
