---
title: "Permisos de clave asimétrica de GRANT (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/12/2017
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
- granting permissions [SQL Server], asymmetric keys
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- GRANT statement, asymmetric keys
ms.assetid: a70e2ee6-59b0-4543-b883-e9cbae6199be
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8c7234246958d82b8c90df9e5ad54d042248cc2d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-asymmetric-key-permissions-transact-sql"></a>GRANT (permisos de clave asimétrica de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede permisos para una clave asimétrica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
GRANT { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
       TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permiso*  
 Especifica un permiso que se puede conceder para una clave asimétrica. Se muestra a continuación.  
  
 CLAVE ASIMÉTRICA **::***asymmetric_key_name*  
 Especifica la clave asimétrica en la que se va a conceder el permiso. Es preciso utilizar el calificador de ámbito "::".  
  
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
 Una clave asimétrica es un elemento protegible de nivel de base de datos que contiene la base de datos que es su entidad primaria en la jerarquía de permisos. A continuación, se enumeran los permisos más específicos y limitados que se pueden conceder para una clave asimétrica, además de los permisos más generales que los incluyen implícitamente.  
  
|Permiso de clave asimétrica|Implícito en el permiso de clave asimétrica|Implícito en el permiso de base de datos|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
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
  
  

