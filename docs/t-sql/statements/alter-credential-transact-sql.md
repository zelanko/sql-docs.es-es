---
title: ALTER CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/19/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER CREDENTIAL
- ALTER_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], credentials
- credentials [SQL Server], ALTER CREDENTIAL statement
- modifying credentials
- authentication [SQL Server], credentials
- ALTER CREDENTIAL statement
ms.assetid: b08899a6-c09e-4af4-91aa-a978ada79264
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d01e5460b01790ba6b7ac59b25e7726399522165
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="alter-credential-transact-sql"></a>ALTER CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de una credencial.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica el nombre de la credencial que se va a modificar.  
  
 IDENTITY **='***identity_name***'**  
 Especifica el nombre de la cuenta que se utilizará para conectarse fuera del servidor.  
  
 SECRET **='***secret***'**  
 Especifica el secreto necesario para la autenticación de salida. *secret* es opcional.  
  
## <a name="remarks"></a>Notas  
 Cuando se cambia una credencial, se restablecen los valores de *identity_name* y *secret*. Si no se especifica el argumento opcional SECRET, el valor del secreto almacenado se establecerá en NULL.  
  
 El secreto está cifrado mediante la clave maestra de servicio. Si se vuelve a generar la clave maestra de servicio, el secreto se vuelve a cifrar utilizando la nueva clave maestra de servicio.  
  
 Puede ver información acerca de las credenciales en la vista de catálogo **sys.credentials**.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY CREDENTIAL. Si la credencial es una credencial del sistema, requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-password-of-a-credential"></a>A. Cambiar la contraseña de una credencial  
 En el siguiente ejemplo se cambia el secreto almacenado en una credencial denominada `Saddles`. La credencial contiene el inicio de sesión de Windows `RettigB` y su contraseña. La nueva contraseña se agrega a la credencial mediante la cláusula SECRET.  
  
```  
ALTER CREDENTIAL Saddles WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. Quitar la contraseña de una credencial  
 En el ejemplo siguiente se quita la contraseña de una credencial denominada `Frames`. La credencial contiene el inicio de sesión de Windows `Aboulrus8` y una contraseña. Después de ejecutar la instrucción, la credencial tendrá una contraseña NULL porque no se especifica la opción SECRET.  
  
```  
ALTER CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
