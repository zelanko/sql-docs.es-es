---
title: Permisos de certificado GRANT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], certificates
- certificates [SQL Server], permissions
- permissions [SQL Server], certificates
- GRANT statement, certificates
ms.assetid: 77270245-a24b-4a20-b481-e6a5ea05b499
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 06cd8f6b6b9e6a05326bad54319961a2120b979d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-certificate-permissions-transact-sql"></a>GRANT (permisos de certificado de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede permisos para un certificado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```
GRANT permission  [ ,...n ]    
    ON CERTIFICATE :: certificate_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *permiso*  
 Especifica un permiso que se puede conceder para un certificado. Se muestra a continuación.  
  
 CERTIFICADO ON **::***nombre_de_certificado*  
 Especifica el certificado en el que se va a conceder el permiso. Es preciso utilizar el calificador de ámbito "::".  
  
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
  
## <a name="remarks"></a>Comentarios  
 Un certificado es un elemento protegible de nivel de base de datos que contiene la base de datos que es su entidad primaria en la jerarquía de permisos. La mayoría de permisos limitados y específicos que se pueden conceder para un certificado se muestran a continuación, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de certificado|Implicado por el permiso de certificado|Implícito en el permiso de base de datos|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CERTIFICATE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 El otorgante del permiso (o la entidad de seguridad especificada con la opción AS) debe tener el permiso con GRANT OPTION, o un permiso superior que implique el permiso que se va a conceder.  
  
 Si se utiliza la opción AS, debe tener en cuenta los requisitos adicionales siguientes.  
  
|AS *granting_principal*|Permiso adicional necesario|  
|------------------------------|------------------------------------|  
|Usuario de la base de datos|Permiso IMPERSONATE para el usuario, pertenencia a la **db_securityadmin** rol fijo de base de datos, la pertenencia a la **db_owner** rol fijo de base de datos, o pertenencia en el **sysadmin** rol fijo de servidor.|  
|Usuario de la base de datos asignado a un inicio de sesión de Windows|Permiso IMPERSONATE para el usuario, pertenencia a la **db_securityadmin** rol fijo de base de datos, la pertenencia a la **db_owner** rol fijo de base de datos, o pertenencia en el **sysadmin** rol fijo de servidor.|  
|Usuario de la base de datos asignado a un grupo de Windows|Pertenencia al grupo de Windows, pertenencia a la **db_securityadmin** rol fijo de base de datos, la pertenencia a la **db_owner** rol fijo de base de datos, o pertenecer el **sysadmin**rol fijo de servidor.|  
|Usuario de la base de datos asignado a un certificado|Pertenencia en el **db_securityadmin** rol fijo de base de datos, la pertenencia a la **db_owner** rol fijo de base de datos, o pertenencia en el **sysadmin** rol fijo de servidor.|  
|Usuario de la base de datos asignado a una clave asimétrica|Pertenencia en el **db_securityadmin** rol fijo de base de datos, la pertenencia a la **db_owner** rol fijo de base de datos, o pertenencia en el **sysadmin** rol fijo de servidor.|  
|Usuario de la base de datos no asignado a una entidad de seguridad del servidor|Permiso IMPERSONATE para el usuario, pertenencia a la **db_securityadmin** rol fijo de base de datos, la pertenencia a la **db_owner** rol fijo de base de datos, o pertenencia en el **sysadmin** rol fijo de servidor.|  
|Rol de base de datos|El permiso ALTER en el rol, pertenencia a la **db_securityadmin** rol fijo de base de datos, la pertenencia a la **db_owner** rol fijo de base de datos, o pertenecer el **sysadmin**rol fijo de servidor.|  
|Rol de aplicación|El permiso ALTER en el rol, pertenencia a la **db_securityadmin** rol fijo de base de datos, la pertenencia a la **db_owner** rol fijo de base de datos, o pertenecer el **sysadmin**rol fijo de servidor.|  
  
 Los propietarios de objetos pueden conceder permisos para los objetos que poseen. Las entidades de seguridad con permiso CONTROL sobre un elemento protegible pueden conceder permisos para ese elemento.  
  
 Los beneficiarios del permiso CONTROL SERVER, como los miembros de la **sysadmin** rol fijo de servidor puede conceder cualquier permiso sobre cualquier elemento protegible en el servidor. Los beneficiarios del permiso CONTROL en una base de datos, como los miembros de la **db_owner** rol fijo de base de datos, puede conceder cualquier permiso sobre cualquier elemento protegible en la base de datos. Los receptores del permiso CONTROL en un esquema pueden conceder los permisos en cualquier objeto del esquema.  
  
## <a name="see-also"></a>Vea también  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Crear rol de aplicación &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

