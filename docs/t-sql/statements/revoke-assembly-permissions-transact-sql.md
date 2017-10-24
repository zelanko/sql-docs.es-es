---
title: REVOCAR permisos de ensamblado (Transact-SQL) | Documentos de Microsoft
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
- REVOKE statement, assemblies
- assemblies [CLR integration], permissions
ms.assetid: f88e9da1-2c0b-4bdd-9ec5-44467707cb46
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0f4fd96d91cd70b51515748a14abc26cd8c857b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-assembly-permissions-transact-sql"></a>REVOKE (permisos de ensamblado de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoca permisos sobre un ensamblado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON ASSEMBLY :: assembly_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 GRANT OPTION FOR  
 Indica que se revocará la capacidad de conceder o denegar el permiso especificado. No se revocará el permiso.  
  
> [!IMPORTANT]  
>  Si la entidad de seguridad dispone del permiso especificado sin la opción GRANT, se revocará el permiso.  
  
 *permiso*  
 Especifica un permiso que se puede revocar para un ensamblado. Se muestra a continuación.  
  
 EN el ENSAMBLADO **::***assembly_name*  
 Especifica el ensamblado para el que se revoca el permiso. El calificador de ámbito **::** es necesario.  
  
 *database_principal*  
 Especifica la entidad de seguridad desde la que se revoca el permiso. Uno de los siguientes:  
  
-   usuario de base de datos  
  
-   rol de base de datos  
  
-   rol de aplicación  
  
-   usuario de base de datos asignado a un inicio de sesión de Windows  
  
-   usuario de base de datos asignado a un grupo de Windows  
  
-   usuario de base de datos asignado a un certificado  
  
-   usuario de base de datos asignado a una clave asimétrica  
  
-   usuario de base de datos no asignado a una entidad de seguridad del servidor  
  
 CASCADE  
 Indica que el permiso que se va a revocar también se revocará de otras entidades de seguridad a las que esta entidad de seguridad ha concedido o denegado permisos.  
  
> [!CAUTION]  
>  Una revocación en cascada de un permiso concedido WITH GRANT OPTION revocará tanto GRANT como DENY de dicho permiso.  
  
 AS *revoking_principal*  
 Especifica una entidad de seguridad de la que la entidad de seguridad que ejecuta esta consulta deriva su derecho de revocar el permiso. Uno de los siguientes:  
  
-   usuario de base de datos  
  
-   rol de base de datos  
  
-   rol de aplicación  
  
-   usuario de base de datos asignado a un inicio de sesión de Windows  
  
-   usuario de base de datos asignado a un grupo de Windows  
  
-   usuario de base de datos asignado a un certificado  
  
-   usuario de base de datos asignado a una clave asimétrica  
  
-   usuario de base de datos no asignado a una entidad de seguridad del servidor  
  
## <a name="remarks"></a>Comentarios  
 Un ensamblado es un elemento protegible de base de datos incluido en la base de datos primaria en la jerarquía de permisos. A continuación, se enumeran los permisos más específicos y limitados que se pueden revocar para un ensamblado, además de los permisos más generales que los incluyen implícitamente.  
  
|Permiso de ensamblado|Implícito en permiso de ensamblado|Implícito en el permiso de base de datos|  
|-------------------------|------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASSEMBLY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL en el ensamblado  
  
## <a name="see-also"></a>Vea también  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREAR ENSAMBLADOS &#40; Transact-SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Crear rol de aplicación &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

