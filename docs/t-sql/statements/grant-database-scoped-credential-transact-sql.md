---
title: GRANT (credencial de ámbito de base de datos de Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- GRANT DATABASE SCOPED CREDENTIAL
- GRANT_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], database scoped credential
- permissions [SQL Server], database scoped credential
- database scoped credential [SQL Server], permissions
- GRANT statement, database scoped credentials
ms.assetid: 501f2c8a-6aeb-41af-bf0b-974d17af33c0
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 865a46c90fb45b6e41dc5ca202133e7b3a22dd53
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633731"
---
# <a name="grant-database-scoped-credential-permissions-transact-sql"></a>GRANT (credencial de ámbito de base de datos de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Concede permisos en una credencial de ámbito de base de datos. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
GRANT permission  [ ,...n ]    
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica un permiso que se puede otorgar en una credencial de ámbito de base de datos. Se muestra a continuación.  
  
 ON DATABASE SCOPED CREDENTIAL **::** _credential_name_  
 Especifica la credencial de ámbito de bases de datos en la que se va a conceder el permiso. Es preciso utilizar el calificador de ámbito "::".  
  
 *database_principal*  
 Especifica la entidad de seguridad para la que se concede el permiso. Uno de los siguientes:  
  
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
 Especifica una entidad de seguridad de la que la entidad de seguridad que ejecuta esta consulta deriva su derecho de conceder el permiso. Uno de los siguientes:  
  
-   usuario de base de datos  
-   rol de base de datos  
-   rol de aplicación  
-   usuario de base de datos asignado a un inicio de sesión de Windows  
-   usuario de base de datos asignado a un grupo de Windows  
-   usuario de base de datos asignado a un certificado  
-   usuario de base de datos asignado a una clave asimétrica  
-   usuario de base de datos no asignado a una entidad de seguridad del servidor  
  
## <a name="remarks"></a>Observaciones  
 Una credencial de ámbito de base de datos es un elemento protegible de nivel de base de datos que contiene la base de datos que es su entidad primaria en la jerarquía de permisos. La mayoría de permisos limitados y específicos que se pueden conceder en una credencial de ámbito de base de datos se muestran aquí abajo, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de credencial de ámbito de base de datos|Implícito en el permiso de credencial de ámbito de base de datos|Implícito en el permiso de base de datos|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permisos  
 El otorgante del permiso (o la entidad de seguridad especificada con la opción AS) debe tener el permiso con GRANT OPTION, o un permiso superior que implique el permiso que se va a conceder.  
  
 Si se utiliza la opción AS, debe tener en cuenta los requisitos adicionales siguientes.  
  
|AS *granting_principal*|Permiso adicional necesario|  
|------------------------------|------------------------------------|  
|Usuario de la base de datos|Permiso IMPERSONATE en el usuario, pertenencia al rol fijo de base de datos **db_securityadmin**, pertenencia al rol fijo de base de datos **db_owner** o pertenencia al rol fijo de servidor **sysadmin**.|  
|Usuario de la base de datos asignado a un inicio de sesión de Windows|Permiso IMPERSONATE en el usuario, pertenencia al rol fijo de base de datos **db_securityadmin**, pertenencia al rol fijo de base de datos **db_owner** o pertenencia al rol fijo de servidor **sysadmin**.|  
|Usuario de la base de datos asignado a un grupo de Windows|Pertenencia al grupo de Windows, pertenencia al rol fijo de base de datos **db_securityadmin**, pertenencia al rol fijo de base de datos **db_owner** o pertenencia al rol fijo de servidor **sysadmin**.|  
|Usuario de la base de datos asignado a un certificado|Pertenencia al rol fijo de base de datos **db_securityadmin**, pertenencia al rol fijo de base de datos **db_owner** o pertenencia al rol fijo de servidor **sysadmin**.|  
|Usuario de la base de datos asignado a una clave asimétrica|Pertenencia al rol fijo de base de datos **db_securityadmin**, pertenencia al rol fijo de base de datos **db_owner** o pertenencia al rol fijo de servidor **sysadmin**.|  
|Usuario de la base de datos no asignado a una entidad de seguridad del servidor|Permiso IMPERSONATE en el usuario, pertenencia al rol fijo de base de datos **db_securityadmin**, pertenencia al rol fijo de base de datos **db_owner** o pertenencia al rol fijo de servidor **sysadmin**.|  
|Rol de base de datos|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos **db_securityadmin**, pertenencia al rol fijo de base de datos **db_owner** o pertenencia al rol fijo de servidor **sysadmin**.|  
|Rol de aplicación|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos **db_securityadmin**, pertenencia al rol fijo de base de datos **db_owner** o pertenencia al rol fijo de servidor **sysadmin**.|  
  
 Los propietarios de objetos pueden conceder permisos para los objetos que poseen. Las entidades de seguridad con permiso CONTROL sobre un elemento protegible pueden conceder permisos para ese elemento.  
  
 Los beneficiarios del permiso CONTROL SERVER, como por ejemplo, los miembros del rol fijo de servidor **sysadmin**, pueden conceder cualquier permiso para cualquier elemento protegible en el servidor. Los beneficiarios del permiso CONTROL para una base de datos, como por ejemplo, los miembros del rol fijo de base de datos **db_owner**, pueden conceder cualquier permiso para cualquier elemento protegible en la base de datos. Los receptores del permiso CONTROL en un esquema pueden conceder los permisos en cualquier objeto del esquema.  
  
## <a name="see-also"></a>Consulte también  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE (credencial de ámbito de base de datos de Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [DENY (credencial de ámbito de base de datos de Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
