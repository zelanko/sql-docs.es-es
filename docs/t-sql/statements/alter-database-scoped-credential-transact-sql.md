---
title: "ALTER CREDENTIAL en el ámbito de base de datos (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 91224c6e96fb3ee3962331ec6f378ea9aad1a5b5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-scoped-credential-transact-sql"></a>CREDENCIAL de ámbito de base de datos de ALTER (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Credencial con ámbito de cambios de las propiedades de una base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica el nombre de la credencial de ámbito de la base de datos que se va a modificar.  
  
 IDENTIDAD **='***identity_name***'**  
 Especifica el nombre de la cuenta que se utilizará para conectarse fuera del servidor. Para importar un archivo de almacenamiento de blobs de Azure, debe ser el nombre de identidad `SHARED ACCESS SIGNATURE`.  Para obtener más información acerca de las firmas de acceso compartido, consulte [firmas de acceso compartido (SAS) usando](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
    
  
 SECRETO **='***secreto***'**  
 Especifica el secreto necesario para la autenticación de salida. *secreto* es necesario para importar un archivo de almacenamiento de blobs de Azure. *secreto* pueden ser opcionales para otros fines.   
>  [!WARNING]
>  El valor de clave de SAS debería comenzar con un '?' (signo de interrogación). Cuando se usa la clave SAS, debe quitar el interlineado '?'. En caso contrario, podrían bloquearse sus esfuerzos.    
  
## <a name="remarks"></a>Comentarios  
 Cuando una base de datos con ámbito de credencial se cambia, los valores de ambos *identity_name* y *secreto* se restablecen. Si no se especifica el argumento opcional SECRET, el valor del secreto almacenado se establecerá en NULL.  
  
 El secreto está cifrado mediante la clave maestra de servicio. Si se vuelve a generar la clave maestra de servicio, el secreto se vuelve a cifrar utilizando la nueva clave maestra de servicio.  
  
 Información sobre las credenciales de ámbito de la base de datos está visible en el [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) vista de catálogo.  
  
## <a name="permissions"></a>Permissions  
 Requiere `ALTER` permiso en la credencial.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. Cambiar la contraseña de una base de datos de credencial con ámbito  
 En el ejemplo siguiente se cambia el secreto almacenado en una credencial de ámbito de la base de datos denominada `Saddles`. La credencial de ámbito de la base de datos contiene el inicio de sesión de Windows `RettigB` y su contraseña. La contraseña nueva se agrega a la credencial de ámbito de la base de datos mediante la cláusula SECRET.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. Quitar la contraseña de una credencial  
 En el ejemplo siguiente se quita la contraseña de una credencial de ámbito de la base de datos denominada `Frames`. La credencial de ámbito de la base de datos contiene el inicio de sesión de Windows `Aboulrus8` y una contraseña. Después de ejecuta la instrucción, la credencial de ámbito de la base de datos tendrá una contraseña NULL porque no se especificó la opción SECRET.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREAR CREDENCIAL en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ELIMINAR CREDENCIALES en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [Sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

