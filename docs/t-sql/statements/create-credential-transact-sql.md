---
title: CREAR CREDENCIAL (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/09/2017
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
- CREDENTIAL_TSQL
- SQL13.SWB.CREDENTIAL.GENERAL.F1
- CREATE CREDENTIAL
- CREATE_CREDENTIAL_TSQL
- CREDENTIAL
dev_langs:
- TSQL
helpviewer_keywords:
- SECRET clause
- authentication [SQL Server], credentials
- CREATE CREDENTIAL statement
- credentials [SQL Server], CREATE CREDENTIAL statement
ms.assetid: d5e9ae69-41d9-4e46-b13d-404b88a32d9d
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 556fa0262696075d63ee549730f2d9824c482dd4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una credencial de nivel de servidor. Una credencial es un registro que contiene la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server. La mayoría de las credenciales incluyen un usuario y una contraseña de Windows. Por ejemplo, guardar una copia de seguridad de base de datos en alguna ubicación podría requerir SQL Server proporcionar credenciales especiales para tener acceso a esa ubicación. Para obtener más información, consulte [credenciales (motor de base de datos)](../../relational-databases/security/authentication-access/credentials-database-engine.md).
  
> [!NOTE]  
>  Para realizar la credencial en el nivel de base de datos de uso [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). Usar una credencial de nivel de servidor cuando necesite usar las mismas credenciales para varias bases de datos en el servidor. Use una credencial de ámbito de base de datos para hacer que la base de datos sea más portátil. Cuando una base de datos se mueve a un nuevo servidor, la credencial de ámbito de la base de datos se moverá con ella. Credenciales con ámbito de base de datos de uso en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
        [ FOR CRYPTOGRAPHIC PROVIDER cryptographic_provider_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica el nombre de la credencial que se va a crear. *credential_name* no se puede iniciar con el signo de número (#). Las credenciales del sistema comienzan por ##.  Cuando se utiliza una firma de acceso compartido (SAS), este nombre debe coincidir con la ruta de acceso de contenedor, comenzar con https y no debe contener una barra diagonal. Vea el ejemplo D a continuación.  
  
 IDENTIDAD **='***identity_name***'**  
 Especifica el nombre de la cuenta que se utilizará para conectarse fuera del servidor. Cuando la credencial se usa para acceder al almacén de claves de Azure, el **identidad** es el nombre del almacén de claves. Vea el ejemplo C más adelante. Cuando la credencial es mediante una firma de acceso compartido (SAS), el **identidad** es *firma de acceso compartido*. Vea el ejemplo D a continuación.  
  
 SECRETO **='***secreto***'**  
 Especifica el secreto necesario para la autenticación de salida.  
  
 Cuando se utiliza la credencial para tener acceso al almacén de claves de Azure la **secreto** argumento de **CREATE CREDENTIAL** requiere el  *\<Id. de cliente >* (sin guiones) y  *\<secreto >* de un **entidad de servicio** en Azure Active Directory que se pasen sin un espacio entre ellos. Vea el ejemplo C más adelante. Cuando la credencial es mediante una firma de acceso compartido, el **secreto** es el token de firma de acceso compartido. Vea el ejemplo D a continuación.  Para obtener información acerca de cómo crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure, consulte [lección 1: crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
 Proveedor de servicios criptográficos *cryptographic_provider_name*  
 Especifica el nombre de un *proveedor de administración de claves (EKM) de empresa*. Para obtener más información acerca de la administración de claves, consulte [administración Extensible de claves &#40; EKM &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Comentarios  

 Si IDENTITY es un usuario de Windows, el secreto puede ser la contraseña. El secreto se cifra usando la clave maestra de servicio. Si se vuelve a generar la clave maestra de servicio, el secreto se vuelve a cifrar con la nueva clave maestra de servicio.  
  
 Después de crear una credencial, puede asignarla a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión mediante el uso de [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) o [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md). A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión se puede asignar a sólo una credencial, pero puede asignar una única credencial a varios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión. Para obtener más información, consulte [credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). Una credencial de nivel de servidor solo puede asignarse a un inicio de sesión, no a un usuario de base de datos. 
  
 Información acerca de las credenciales es visible en el [sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) vista de catálogo.  
  
 Si no hay ninguna credencial de inicio de sesión asignada para el proveedor, se utiliza la credencial asignada a la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Un inicio de sesión puede tener asignadas varias credenciales, siempre y cuando se utilicen con proveedores distintos. Solo debe haber una credencial asignada por cada proveedor y por cada inicio de sesión. La misma credencial puede estar asignada a otros inicios de sesión.  
  
## <a name="permissions"></a>Permissions  
 Requiere **ALTER ANY CREDENTIAL** permiso.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-basic-example"></a>A. Ejemplo básico  
 En el ejemplo siguiente se crea la credencial denominada `AlterEgo`. La credencial contiene el usuario de Windows `Mary5` y una contraseña.  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>B. Crear una credencial de EKM  
 En el ejemplo siguiente se utiliza una cuenta creada previamente denominada `User1OnEKM` en un módulo EKM a través de las herramientas de administración de EKM, con un tipo de cuenta y una contraseña básicos. El **sysadmin** cuenta en el servidor crea una credencial que se usa para conectarse a la cuenta EKM y lo asigna a la `User1` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta:  
  
```  
CREATE CREDENTIAL CredentialForEKM  
    WITH IDENTITY='User1OnEKM', SECRET='<EnterStrongPasswordHere>'  
    FOR CRYPTOGRAPHIC PROVIDER MyEKMProvider;  
GO  
  
/* Modify the login to assign the cryptographic provider credential */  
ALTER LOGIN Login1  
ADD CREDENTIAL CredentialForEKM;  
  
/* Modify the login to assign a non cryptographic provider credential */   
ALTER LOGIN Login1  
WITH CREDENTIAL = AlterEgo;  
GO  
```  
  
### <a name="c-creating-a-credential-for-ekm-using-the-azure-key-vault"></a>C. Crear una credencial de EKM con Azure Key Vault  
 En el ejemplo siguiente se crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] credencial para la [!INCLUDE[ssDE](../../includes/ssde-md.md)] a usar al obtener acceso el almacén de claves de Azure utilizando el **conector de SQL Server para el almacén de claves de Microsoft Azure**. Para obtener un ejemplo completo del uso de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conector, consulte [Extensible administración utilizando Azure clave de almacén de claves &#40; SQL Server &#41; ](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  El argumento **IDENTITY** de **CREATE CREDENTIAL** requiere el nombre del Almacén de claves. El **secreto** argumento de **CREATE CREDENTIAL** requiere el  *\<Id. de cliente >* (sin guiones) y  *\<secreto >*  se pasen juntos sin un espacio entre ellos.  
  
 En el ejemplo siguiente, el **Id. de cliente** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) se deja sin guiones y se introduce como la cadena `EF5C8E094D2A4A769998D93440D8115D` . El **secreto** se representa con la cadena *SECRET_DBEngine*.  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 En el ejemplo siguiente se crea la misma credencial al usar variables para el **Id. de cliente** y **secreto** cadenas, ya que, a continuación, se concatenan juntos para formar la **secreto** argumento pasado. El **reemplazar** función se utiliza para quitar los guiones del ID de cliente.  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>D. Crear una credencial utilizando un Token de SAS  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 En el ejemplo siguiente se crea una credencial de firma de acceso compartido con un token SAS.  Para obtener un tutorial sobre cómo crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure y, a continuación, crear una credencial mediante la firma de acceso compartido, consulte [Tutorial: usar el servicio de almacenamiento de blobs de Microsoft Azure con SQL Server 2016 las bases de datos](Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases.md).  
  
> [!IMPORTANT]  
>  EL **nombre de CREDENCIAL** argumento requiere que el nombre coincide con la ruta de acceso de contenedor, empiece con https y no contienen una barra diagonal. El **identidad** argumento requiere el nombre, *firma de acceso compartido*. El **secreto** argumento requiere que el token de firma de acceso compartido.  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>Vea también  
 [Credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [CREAR CREDENCIAL en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Lección 2: Crear una credencial de SQL Server mediante una firma de acceso compartido](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [Firmas de acceso compartido](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  

