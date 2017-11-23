---
title: "REVOCAR permisos de clave asimétrica (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- REVOKE statement, asymmetric keys
ms.assetid: 1a1063e8-ffc7-4775-a40d-e155740ad7b2
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae298d40c75f35df8ed93c850ecadd797155656b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-asymmetric-key-permissions-transact-sql"></a>REVOKE (permisos de clave asimétrica de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Revoca los permisos de una clave asimétrica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REVOKE [ GRANT OPTION FOR ] { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 GRANT OPTION FOR  
 Indica que se revocará la capacidad de conceder el permiso especificado.  
  
> [!IMPORTANT]  
>  Si la entidad de seguridad dispone del permiso especificado sin la opción GRANT, se revocará el permiso.  
  
 *permiso*  
 Especifica un permiso que se puede revocar para un ensamblado. Se muestra a continuación.  
  
 CLAVE ASIMÉTRICA **::***asymmetric_key_name*  
 Especifica la clave asimétrica en la que se va a revocar el permiso. El calificador de ámbito **::** es necesario.  
  
 *database_principal*  
 Especifica la entidad de seguridad desde la que se revoca el permiso. Uno de los siguientes:  
  
-   Usuario de la base de datos  
  
-   Rol de base de datos  
  
-   Rol de aplicación  
  
-   Usuario de la base de datos asignado a un inicio de sesión de Windows  
  
-   Usuario de la base de datos asignado a un grupo de Windows  
  
-   Usuario de la base de datos asignado a un certificado  
  
-   Usuario de la base de datos asignado a una clave asimétrica  
  
-   Usuario de la base de datos no asignado a una entidad de seguridad de servidor.  
  
 CASCADE  
 Indica que el permiso que se va a revocar también se revocará de otras entidades de seguridad a las que esta entidad de seguridad ha concedido o denegado permisos. No se revocará el permiso.  
  
> [!CAUTION]  
>  Una revocación en cascada de un permiso concedido WITH GRANT OPTION revocará tanto GRANT como DENY de dicho permiso.  
  
 AS *revoking_principal*  
 Especifica una entidad de seguridad de la que la entidad de seguridad que ejecuta esta consulta deriva su derecho de revocar el permiso. Uno de los siguientes:  
  
-   Usuario de la base de datos  
  
-   Rol de base de datos  
  
-   Rol de aplicación  
  
-   Usuario de la base de datos asignado a un inicio de sesión de Windows  
  
-   Usuario de la base de datos asignado a un grupo de Windows  
  
-   Usuario de la base de datos asignado a un certificado  
  
-   Usuario de la base de datos asignado a una clave asimétrica  
  
-   Usuario de la base de datos no asignado a una entidad de seguridad de servidor.  
  
## <a name="remarks"></a>Comentarios  
 Una clave asimétrica es un elemento protegible de nivel de base de datos que contiene la base de datos que es su entidad primaria en la jerarquía de permisos. La mayoría de permisos limitados y específicos que se pueden revocar en una clave asimétrica se muestran a continuación, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de clave asimétrica|Implícito en el permiso de clave asimétrica|Implícito en el permiso de base de datos|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 Requiere permiso CONTROL en la clave asimétrica.  
  
## <a name="see-also"></a>Vea también  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Crear rol de aplicación &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
