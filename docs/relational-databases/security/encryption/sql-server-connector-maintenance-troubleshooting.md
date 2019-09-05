---
title: Mantenimiento y solución de problemas del conector de SQL Server| Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
author: aliceku
ms.author: aliceku
ms.openlocfilehash: d24f4e86f59e91537886480b26248c683665850a
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "70148779"
---
# <a name="sql-server-connector-maintenance-amp-troubleshooting"></a>Mantenimiento y solución de problemas del conector de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se proporciona información adicional acerca del conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información acerca del conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Administración extensible de claves con el Almacén de claves de Azure & #40; SQL Server & #41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md), [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md) (Pasos de instalación de Administración extensible de claves con el Almacén de claves de Azure) y [Use SQL Server Connector with SQL Encryption Features](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md) (Usar el conector de SQL Server con características de cifrado de SQL).  
  
  
##  <a name="AppendixA"></a> A. Instrucciones de mantenimiento para el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
### <a name="key-rollover"></a>Sustitución incremental de claves  
  
> [!IMPORTANT]  
>  El conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere que el nombre de clave solo use los caracteres "a-z", "A-Z", "0-9" y "-", con un límite de 26 caracteres.   
> No funcionará el uso de diferentes versiones de claves bajo el mismo nombre de clave en el Almacén de claves de Azure con el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para girar una clave de Azure Key Vault que está usando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se debe crear una clave con un nombre de clave nuevo.  
  
 Normalmente se necesita crear versiones de las claves asimétricas de servidor para cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cada 1 o 2 años. Es importante tener en cuenta que aunque el Almacén de claves permite versiones de clave, los clientes no deben usar esta característica para implementar el control de versiones. El conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se puede ocupar de los cambios en la versión de clave del Almacén de claves. Para implementar el control de versiones de claves, el cliente debe crear una nueva clave en el Almacén de claves y volver a cifrar la clave de cifrado de datos en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
 Para TDE, así es cómo se lograría:  
  
-   **En PowerShell:** cree una nueva clave asimétrica (con un nombre diferente de la clave asimétrica de TDE actual) en Key Vault.  
  
    ```powershell  
    Add-AzKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
-   **Con [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] o sqlcmd.exe:** use las siguientes instrucciones, como se muestra en el paso 3 de la sección 3.  
  
     Importe la nueva clave asimétrica.  
  
    ```sql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]   
    FROM PROVIDER [EKM]   
    WITH PROVIDER_KEY_NAME = 'Key2',   
    CREATION_DISPOSITION = OPEN_EXISTING   
    GO  
    ```  
  
     Cree un nuevo inicio de sesión que se asociará con la nueva clave asimétrica (como se muestra en las instrucciones de TDE).  
  
    ```sql  
    USE master  
    CREATE LOGIN TDE_Login2   
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     Cree una nueva credencial para asignarse al inicio de sesión.  
  
    ```sql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',   
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789='   
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     Elija la base de datos cuya clave de cifrado de base de datos le gustaría volver a cifrar.  
  
    ```sql  
    USE [database]  
    GO  
    ```  
  
     Vuelva a cifrar la clave de cifrado de la base de datos.  
  
    ```sql  
    ALTER DATABASE ENCRYPTION KEY   
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-includessnoversionincludesssnoversion-mdmd-connector"></a>Actualización del conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

Las versiones 1.0.0.440 y anteriores se han reemplazado y ya no se admiten en entornos de producción. Las versiones 1.0.1.0 y posteriores se admiten en los entornos de producción. Use las instrucciones siguientes para actualizar a la versión más reciente disponible en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=45344).

Si actualmente usa la versión 1.0.1.0 o posterior, siga estos pasos para actualizar a la versión más reciente del Conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Estas instrucciones evitan la necesidad de reiniciar la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .
 
1. Instale la versión más reciente del Conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde el [Centro de descargas de Microsoft](https://www.microsoft.com/download/details.aspx?id=45344). En el asistente de instalación, guarde el archivo DLL nuevo en una ruta de acceso a archivo distinta de la ruta de acceso a archivo del DLL del Conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] original. Por ejemplo, la nueva ruta de acceso archivo podría ser la siguiente: `C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll`
 
2. En la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ejecute el siguiente comando Transact-SQL para dirigir la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la versión nueva del Conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :

    ``` 
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll'
    GO  
    ```

Si actualmente usa la versión 1.0.0.440 o anterior, siga estos pasos para actualizar a la versión más reciente del Conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .
  
1.  Detenga la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  Detenga el servicio del conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
3.  Desinstalar el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la característica Programas y características de Windows.  
  
     (Como alternativa, puede cambiar el nombre de la carpeta en la que se encuentra el archivo DLL). El nombre predeterminado de la carpeta es "[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para Microsoft Azure Key Vault".  
  
4.  Instale la versión más reciente del conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde el Centro de descargas de Microsoft.  
  
5.  Reinicie la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
6.  Ejecute la siguiente instrucción para modificar el proveedor de EKM y comenzar a usar la versión más reciente del conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Asegúrese de que la ruta del archivo apunte a donde descargó la versión más reciente. (Se puede omitir este paso si se instala la nueva versión en la misma ubicación que la versión original). 
  
    ```sql  
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
7.  Compruebe que las bases de datos con TDE sean accesibles.  
  
8.  Después de comprobar que la actualización funciona, puede eliminar la antigua carpeta del conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (si decide cambiar el nombre en lugar de desinstalar en el paso 3).  
  
### <a name="rolling-the-includessnoversionincludesssnoversion-mdmd-service-principal"></a>Puesta en marcha de la entidad de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa entidades de servicio creadas en Azure Active Directory como credenciales para acceder al Almacén de claves.  La entidad de servicio tiene identificador de cliente y clave de autenticación.  Una credencial de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se configura con el **nombre de almacén**, el **identificador de cliente**y la **clave de autenticación**.  La **clave de autenticación** es válida durante un determinado período de tiempo (uno o dos años).   Antes de que expire el período de tiempo se debe generar una nueva clave en Azure AD para la entidad de servicio.  Después, la credencial debe cambiarse en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].    [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] mantiene una caché para la credencial en la sesión actual, por lo que cuando se cambia una credencial, [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] se debe reiniciar.  
  
### <a name="key-backup-and-recovery"></a>Copia de seguridad y recuperación de claves  
Se debe realizar una copia de seguridad del almacén de claves con cierta frecuencia. Si se pierde una clave asimétrica en el almacén, se puede restaurar desde la copia de seguridad. La clave debe restaurarse con el mismo nombre que antes, que es lo que hará el comando de PowerShell Restore (consulte los pasos siguientes).  
Si el almacén se ha perdido, tendrá que volver a crear un almacén y restaurar la clave asimétrica en el almacén usando el mismo nombre que antes. El nombre del almacén puede ser diferente (o el mismo que antes). También debe establecer los permisos de acceso en el nuevo almacén para conceder a la entidad de servicio de SQL Server el acceso necesario para los escenarios de cifrado de SQL Server y ajustar la credencial de SQL Server para que se refleje el nuevo nombre del almacén .

En resumen, estos son los pasos:  
  
* Realice una copia de seguridad de la clave del almacén (con el cmdlet de Powershell Backup-AzureKeyVaultKey).  
* En caso de error del almacén, cree un nuevo almacén en la misma región geográfica*. El usuario que crea esto debería estar en el mismo directorio predeterminado que el programa de instalación de la entidad de servicio para SQL Server.  
* Restaure la clave en el nuevo almacén (mediante el cmdlet Restore-AzureKeyVaultKey de Powershell; esto restaura la clave con el mismo nombre que antes). Si ya existe una clave con el mismo nombre, se producirá un error en la restauración.  
* Conceda permisos a la entidad de servicio de SQL Server para que use este nuevo almacén.  
* Modifique la credencial de SQL Server que usa el motor de base de datos para reflejar el nuevo nombre de almacén (si es necesario).  
  
Las copias de seguridad de claves se pueden restaurar entre regiones de Azure, siempre que permanezcan en la misma región geográfica o nube nacional: Estados Unidos, Canadá, Japón, Australia, India, APAC, Europa, Brasil, China, US Government o Alemania.  
  
  
##  <a name="AppendixB"></a> B. Preguntas más frecuentes  
### <a name="on-azure-key-vault"></a>En el Almacén de claves de Azure  
  
**¿Cómo funcionan las operaciones de clave con el Almacén de claves de Azure?**  
 La clave asimétrica en el Almacén de claves se usa para proteger las claves de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La parte pública de la clave asimétrica es la única que sale del almacén: el almacén no exporta nunca la parte privada. Todas las operaciones de cifrado en las que se usa la clave asimétrica se realizan en el servicio Azure Key Vault y se protegen con la seguridad del servicio.  
  
 **¿Qué es un URI de clave?**  
 Todas las claves del Almacén de claves de Azure tienen un identificador uniforme de recursos, (URI), que se puede usar para hacer referencia a la clave en la aplicación. Use el formato `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` para obtener la versión actual y el formato `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` para obtener una versión específica.  
  
### <a name="on-configuring-includessnoversionincludesssnoversion-mdmd"></a>Configuración [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**¿Qué son los extremos a los que necesita tener acceso el conector de SQL Server?** El conector se comunica con dos extremos, que deben estar en una lista blanca. El único puerto requerido para la comunicación saliente a estos otros servicios es el puerto 443 para Https:
-  login.microsoftonline.com/*:443
-  *.vault.azure.net/* :443
  
**¿Cuáles son los niveles de permiso mínimos necesarios para cada paso de configuración en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]?**  
 Aunque puede realizar todos los pasos de configuración como miembro del rol fijo de servidor sysadmin, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] le anima a minimizar los permisos que usa. En la lista siguiente se define el nivel de permiso mínimo para cada acción.  
  
-   Para crear un proveedor de servicios criptográficos, son necesarios el permiso `CONTROL SERVER` o la pertenencia al rol fijo de servidor **sysadmin** .  
  
-   Para cambiar una opción de configuración y ejecutar la instrucción de `RECONFIGURE` , debe tener concedido el permiso `ALTER SETTINGS` de nivel de servidor. Los roles fijos de servidor sysadmin y `ALTER SETTINGS` serveradmin **tienen el permiso** de forma implícita.  
  
-   Para cread una credencial, necesita el permiso `ALTER ANY CREDENTIAL` .  
  
-   Para agregar una credencial a un inicio de sesión, necesita el permiso `ALTER ANY LOGIN` .  
  
-   Para crear una clave asimétrica, necesita el permiso `CREATE ASYMMETRIC KEY` .  

**¿Cómo puedo cambiar el Active Directory predeterminado para que mi almacén de claves se cree en la misma suscripción y Active Directory de la entidad de servicio que creé para el Conector de [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] ?**

![aad-change-default-directory-helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. Vaya al portal clásico de Azure: [https://manage.windowsazure.com](https://manage.windowsazure.com).  
2. En el menú de la izquierda, desplácese hacia abajo y seleccione **Configuración**.
3. Seleccione la suscripción a Azure que usa actualmente y haga clic en **Editar directorio** en los comandos que aparecen en la parte inferior de la pantalla.
4. En la ventana emergente, use el menú desplegable **Directorio** para seleccionar el Active Directory que desea usar. Esto lo convertirá en el directorio predeterminado.
5. Asegúrese de ser el administrador global del Active Directory recién seleccionado. Si no es el administrador global, podría perder permisos de administración después del cambio de directorios.
6. Una vez que se cierra la ventana emergente, si no ve ninguna de las suscripciones, puede que tenga que actualizar el filtro **Filtrar por directorio** del filtro **Suscripciones** en el menú superior derecho de la pantalla para ver las suscripciones que usa la instancia de Active Directory recién seleccionada.

    > [!NOTE] 
    > Puede que no tenga los permisos para realmente cambiar el directorio predeterminado de la suscripción a Azure. En este caso, cree la entidad de servicio de AAD dentro del directorio predeterminado para que esté en el mismo directorio que Azure Key Vault que se usará más adelante.

Para más información sobre Active Directory, consulte [Asociación de las suscripciones de Azure con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-how-subscriptions-associated-directory/).
  
##  <a name="AppendixC"></a> C. Explicación de los códigos de error para el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 **Códigos de error del proveedor:**  
  
Código de error  |Símbolo  |Descripción    
---------|---------|---------  
0 | scp_err_Success | La operación se ha realizado correctamente.    
1 | scp_err_Failure | Se produjeron errores en la operación.    
2 | scp_err_InsufficientBuffer | Este error indica al motor que asigne más memoria para el búfer.    
3 | scp_err_NotSupported | La operación no es compatible. Por ejemplo, el tipo de clave o el algoritmo especificado no es compatible con el proveedor EKM.    
4 | scp_err_NotFound | El proveedor EKM no ha podido encontrar el algoritmo o la clave especificada.    
5 | scp_err_AuthFailure | Error durante la autenticación con el proveedor EKM.    
6 | scp_err_InvalidArgument | El argumento proporcionado no es válido.    
7 | scp_err_ProviderError | Se ha producido un error sin especificar en el proveedor EKM que ha detectado el motor de SQL.    
2049 | scp_err_KeyNameDoesNotFitThumbprint | El nombre de la clave es demasiado largo para caber en la huella digital del motor de SQL. El nombre de la clave no debe superar los 26 caracteres.    
2050 | scp_err_PasswordTooShort | La cadena de secreto, que es la concatenación del identificador de cliente y el secreto de AAD, no llega a 32 caracteres.    
2051 | scp_err_OutOfMemory | El motor de SQL se ha quedado sin memoria y no se ha podido asignar la memoria para el proveedor EKM.    
2052 | scp_err_ConvertKeyNameToThumbprint | No se ha podido convertir el nombre de la clave en una huella digital.    
2053 | scp_err_ConvertThumbprintToKeyName|  No se ha podido convertir la huella digital en un nombre de clave.    
3000 | ErrorSuccess | La operación de AKV se ha realizado correctamente.    
3001 | ErrorUnknown | Se ha producido un error en la operación de AKV con un error sin especificar.    
3002 | ErrorHttpCreateHttpClientOutOfMemory | No se puede crear un elemento HttpClient para la operación de AKV debido a que no hay memoria suficiente.    
3003 | ErrorHttpOpenSession | No se puede abrir una sesión Http debido a un error de red.    
3004 | ErrorHttpConnectSession | No se puede conectar una sesión Http debido a un error de red.    
3005 | ErrorHttpAttemptConnect | No se puede intentar una conexión debido a un error de red.    
3006 | ErrorHttpOpenRequest | No se puede abrir una solicitud debido a un error de red.    
3007 | ErrorHttpAddRequestHeader | No se puede agregar un encabezado de solicitud.    
3008 | ErrorHttpSendRequest | No se puede enviar una solicitud debido a un error de red.    
3009 | ErrorHttpGetResponseCode | No se puede obtener un código de respuesta debido a un error de red.    
3010 | ErrorHttpResponseCodeUnauthorized | El servidor ha respondido con el error 401 a la solicitud.    
3011 | ErrorHttpResponseCodeThrottled | El servidor ha limitado la solicitud.    
3012 | ErrorHttpResponseCodeClientError | La solicitud que se envió desde el conector no es válida. Normalmente esto significa que el nombre de clave no es válido o contiene caracteres no válidos.
3013 | ErrorHttpResponseCodeServerError | El servidor ha respondido con un código de respuesta entre 500 y 600.    
3014 | ErrorHttpQueryHeader | No se puede realizar una consulta para el encabezado de respuesta.    
3015 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader | No se puede copiar el encabezado de respuesta debido a que no hay memoria suficiente.    
3016 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer | No se puede realizar una consulta al encabezado de respuesta debido a que no hay memoria suficiente al reasignar un búfer.    
3017 | ErrorHttpQueryHeaderNotFound | No se encuentra el encabezado de consulta en la respuesta.    
3018 | ErrorHttpQueryHeaderUpdateBufferLength | No se puede actualizar la longitud del búfer al realizar una consulta del encabezado de respuesta.    
3019 | ErrorHttpReadData | No se pueden leer los datos de respuesta debido a un error de red. 
3076 | ErrorHttpResourceNotFound | El servidor respondió con un error 404 porque no se encontró el nombre de clave. Asegúrese de que el nombre de la clave existe en el almacén.
3077 | ErrorHttpOperationForbidden | El servidor respondió con un error 403 porque el usuario no tiene el permiso adecuado para realizar la acción. Asegúrese de que tiene el permiso para la operación especificada. Como mínimo, el conector requiere los permisos 'get, list, wrapKey, unwrapKey' para funcionar adecuadamente.   
  
Si no ve el código de error en esta tabla, estas son algunas razones más por las que se puede estar produciendo el error:   
  
-   No dispone de acceso a Internet y no puede acceder a la instancia de Azure Key Vault. Compruebe la conexión a Internet.  
  
-   Es posible que el servicio del Almacén de claves de Azure esté fuera de servicio. Vuelva a intentarlo en otro momento.  
  
-   Es posible que haya quitado la clave asimétrica del Almacén de datos de Azure o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Restaure la clave.  
  
-   Si recibe un error de "No se puede cargar la biblioteca", asegúrese de tener la versión adecuada de Visual Studio C++ Redistribuible instalada en función de la versión de SQL Server que se esté ejecutando. En la tabla siguiente se especifica qué versión instalar desde el Centro de descarga de Microsoft.   
  
Versión de SQL Server  |Vínculo de instalación redistribuible    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Paquetes redistribuibles de Visual C++ para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual C++ Redistributable para Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
  
  
## <a name="additional-references"></a>Referencias adicionales  
 Más información acerca de la Administración extensible de claves:  
  
-   [Administración extensible de claves &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 Cifrados de SQL compatibles con EKM:  
  
-   [Habilitar TDE en SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
-   [Cifrado de copia de seguridad](../../../relational-databases/backup-restore/backup-encryption.md)  
  
-   [Crear una copia de seguridad cifrada](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 Comandos de [!INCLUDE[tsql](../../../includes/tsql-md.md)] relacionados:  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Documentación del Almacén de claves de Azure:  
  
-   [¿Qué es el Almacén de claves de Azure?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)  
  
-   [Introducción al Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)  
  
-   Referencia de [cmdlets del Almacén de claves de Azure](/powershell/module/azurerm.keyvault/) de PowerShell  
  
## <a name="see-also"></a>Consulte también

 [Administración extensible de claves con Azure Key Vault](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [Usar el conector de SQL Server con características de cifrado de SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)  
 [EKM provider enabled (opción de configuración del servidor)](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
 [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)
