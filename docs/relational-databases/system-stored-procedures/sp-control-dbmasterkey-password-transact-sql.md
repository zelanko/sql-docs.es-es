---
title: sp_control_dbmasterkey_password (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 02/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8564e7fc3ab9f9e6419ebe7ff140408cb1940b29
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spcontroldbmasterkeypassword-transact-sql"></a>sp_control_dbmasterkey_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega o quita una credencial que contiene la contraseña necesaria para abrir la clave maestra de una base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>Argumentos  
 @db_name= N'*database_name*'  
 Especifica el nombre de la base de datos asociada a esta credencial. No puede ser una base de datos del sistema. *database_name* es **nvarchar**.  
  
 @password= N'*contraseña*'  
 Especifica la contraseña de la clave maestra. *contraseña* es **nvarchar**.  
  
 @action= N'add'  
 Especifica que se agregará al almacén de credenciales una credencial para la base de datos especificada. La credencial contendrá la contraseña de la clave maestra de la base de datos. El valor pasado a @action es **nvarchar**.  
  
 @action= N'drop'  
 Especifica que se quitará del almacén de credenciales una credencial para la base de datos especificada. El valor pasado a @action es **nvarchar**.  
  
## <a name="remarks"></a>Comentarios  
 Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesita la clave maestra de una base de datos para cifrar o descifrar una clave, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentará descifrar la clave maestra de la base de datos con la clave maestra de servicio de la instancia. Si el descifrado produce errores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] buscará en el almacén de credenciales las credenciales de clave maestra con el mismo GUID de familia que la base de datos para la que se necesita la clave maestra. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentará después descifrar la clave maestra de la base de datos con cada credencial coincidente hasta que el descifrado se realice correctamente o no queden más credenciales.  
  
> [!CAUTION]  
>  No cree una credencial de clave maestra para una base de datos que deba estar inaccesible para sa y otras entidades de seguridad de servidor con numerosos privilegios. Puede configurar una base de datos de forma que su jerarquía de claves no pueda descifrarse con la clave maestra de servicio. Esta opción se admite como una defensa para bases de datos que contienen información cifrada que no debe estar accesible para sa u otras entidades de seguridad de servidor con amplios privilegios. Al crear una credencial de clave maestra para esta base de datos se quita la defensa, por lo que sa y otras entidades de seguridad de servidor con numerosos privilegios podrán descifrar la base de datos.  
  
 Las credenciales creadas mediante sp_control_dbmasterkey_password están visibles en el [sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md) vista de catálogo. Los nombres de las credenciales creadas para las claves maestras de base de datos presentan el siguiente formato: `##DBMKEY_<database_family_guid>_<random_password_guid>##`. La contraseña se almacena como el secreto de la credencial. Para cada contraseña que se agrega al almacén de credenciales hay una fila en sys.credentials.  
  
 No puede utilizar sp_control_dbmasterkey_password para crear una credencial para las siguientes bases de datos del sistema: maestra, model, msdb, o tempdb.  
  
 sp_control_dbmasterkey_password no comprueba si la contraseña puede abrir la clave maestra de la base de datos especificada.  
  
 Si especifica una contraseña ya almacenada en una credencial para la base de datos especificada, sp_control_dbmasterkey_password registrará errores.  
  
> [!NOTE]  
>  Dos bases de datos de diferentes instancias de servidor pueden compartir el mismo GUID de familia. Si esto ocurriera, las bases de datos compartirían los mismos registros de clave maestra en el almacén de credenciales.  
  
 Los parámetros que se pasan a sp_control_dbmasterkey_password no se muestran en seguimientos.  
  
> [!NOTE]  
>  Cuando utiliza la credencial que se agregó mediante sp_control_dbmasterkey_password para abrir la clave maestra de la base de datos, la clave maestra de servicio vuelve a cifrar la clave maestra de la base de datos. Si la base de datos está en modo de solo lectura, se producirá un error en la operación de recifrado y la clave maestra de la base de datos permanecerá sin cifrar. Para el acceso subsiguiente a la clave maestra de la base de datos debe utilizar la instrucción OPEN MASTER KEY y una contraseña. Para evitar el uso de una contraseña, cree la credencial antes de pasar la base de datos al modo de solo lectura.  
  
 **Posible problema de compatibilidad con versiones anteriores:** actualmente, el procedimiento almacenado no comprueba si existe una clave maestra. Esto se admite por cuestiones de compatibilidad con versiones anteriores, pero muestra una advertencia. Este comportamiento se ha desaprobado. En una versión futura de la clave maestra debe existir y la contraseña utilizada en el procedimiento almacenado **sp_control_dbmasterkey_password** debe ser la misma contraseña que una de las contraseñas utilizadas para cifrar la clave maestra de base de datos.  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso CONTROL en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>A. Crear una credencial para la clave maestra de AdventureWorks2012  
 En el siguiente ejemplo se crea una credencial para la clave maestra de la base de datos `AdventureWorks2012` y se guarda la contraseña de la clave maestra como secreto en la credencial. Dado que todos los parámetros que se pasan a `sp_control_dbmasterkey_password` debe ser del tipo de datos **nvarchar**, las cadenas de texto se convierten con el operador de conversión `N`.  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'add';  
GO  
```  
  
### <a name="b-dropping-a-credential-for-a-database-master-key"></a>B. Quitar una credencial para la clave maestra de una base de datos  
 En el siguiente ejemplo se quita la credencial creada en el ejemplo A. Tenga en cuenta que son necesarios todos los parámetros, incluida la contraseña.  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'drop';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Establecer una base de datos reflejada cifrada](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [Seguridad almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
