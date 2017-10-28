---
title: "Pasos de instalación de Administración extensible de claves con Azure Key Vault | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8b6ddedabeb826caf903701327b6b103666b2abb
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="setup-steps-for-extensible-key-management-using-the-azure-key-vault"></a>Setup Steps for Extensible Key Management Using the Azure Key Vault (Pasos de instalación de Administración extensible de claves con el Almacén de claves de Azure)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Los siguientes pasos le indican cómo realizar la instalación y configuración del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]conector para el Almacén de claves de Azure.  
  
## <a name="before-you-start"></a>Antes de empezar  
 Para usar el Almacén de claves de Azure con su SQL Server, tiene que cumplir los siguientes requisitos previos:  
  
-   Debe tener una suscripción de Azure  
  
-   Instale la última versión de [Azure PowerShell](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/) (1.0.1 o superior).  

-   Crear un Azure Active Directory  

-   Familiarícese con las entidades de seguridad del almacenamiento de EKM con el Almacén de claves de Azure. Para ello, revise [Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md) (Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;).  

-   Debe tener la versión adecuada de Visual Studio C++ redistribuible instalada basándose en la versión de SQL Server que está ejecutando:
  
Versión de SQL Server  |Vínculo de instalación redistribuible    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Paquetes redistribuibles de Visual C++ para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual C++ Redistributable para Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="part-i-set-up-an-azure-active-directory-service-principal"></a>Parte I: Configurar una entidad de servicio de Active Directory de Azure  
 Para conceder permisos de acceso a SQL Server a su Almacén de claves de Azure, necesitará una cuenta de entidad de servicio en Azure Active Directory (AAD).  
  
1.  Vaya al [portal clásico de Azure](https://manage.windowsazure.com)e inicie sesión.  
  
2.  Registre una aplicación con Azure Active Directory. Para obtener instrucciones pormenorizadas para registrar una aplicación, vea la sección **Get an identity for the application** (Obtener una identidad para la aplicación) de la [publicación del blog de Almacén de claves de Azure](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/).  
  
3.  Copie el **id. de cliente** y el **secreto de cliente** para un paso posterior, en el que se usarán para otorgar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acceso a su Almacén de claves.  
  
 ![ekm-client-id](../../../relational-databases/security/encryption/media/ekm-client-id.png "ekm-client-id")  
  
 ![ekm-key-id](../../../relational-databases/security/encryption/media/ekm-key-id.png "ekm-key-id")  
  
## <a name="part-ii-create-a-key-vault-and-key"></a>Parte II: Crear un almacén de claves y una clave  
 El motor de base de datos de SQL Server usará el almacén de claves y la clave creados aquí para la protección de claves de cifrado.  
  
> [!IMPORTANT]  
>  La suscripción en la que se crea el almacén de claves debe estar en el mismo Azure Active Directory predeterminado en el que se creó la entidad de servicio de Azure Active Directory. Si desea usar un Active Directory distinto del Active Directory predeterminado para crear una entidad de servicio para el Conector de SQL Server, debe cambiar el Active Directory predeterminado en la cuenta de Azure antes de crear el almacén de claves. Para información sobre cómo cambiar el Active Directory predeterminado al que desea usar, consulte las [Preguntas más frecuentes](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)sobre el Conector de SQL Server.  
  
1.  **Abrir PowerShell e iniciar sesión**  
  
     Instale e inicie la última versión de [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) (1.0.1 o superior). Inicie sesión en su cuenta de Azure con el siguiente comando:  
  
    ```powershell  
    Login-AzureRmAccount  
    ```  
  
     La instrucción devuelve:  
  
    ```  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    >  Si tiene varias suscripciones y desea especificar una en concreto para usar con el almacén, use `Get-AzureRmSubscription` para ver las suscripciones y `Select-AzureRmSubscription` para elegir la suscripción correcta. De lo contrario, PowerShell seleccionará una de forma predeterminada.  
  
2.  **Crear un nuevo grupo de recursos**  
  
     Todos los recursos de Azure creados mediante Azure Resource Manager deben estar contenidos en grupos de recursos. Cree un grupo de recursos para alojar el almacén de claves. En este ejemplo se usa `ContosoDevRG`. Elija su propio grupo de recursos **único** y el nombre del almacén de claves, ya que todos los nombres de almacén de claves son únicos y globales.  
  
    ```powershell  
    New-AzureRmResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
     La instrucción devuelve:  
  
    ```  
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :   
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]  
    >  Para el `-Location parameter`, use el comando `Get-AzureLocation` para identificar cómo especificar una ubicación alternativa a la de este ejemplo. Si necesita más información, escriba: `Get-Help Get-AzureLocation`  
  
3.  **Crear un almacén de claves**  
  
     El cmdlet `New-AzureRmKeyVault` requiere un nombre de grupo de recursos, un nombre de almacén de claves y una ubicación geográfica. Por ejemplo, para un almacén de claves denominado `ContosoDevKeyVault`, escriba:  
  
    ```powershell  
    New-AzureRmKeyVault -VaultName 'ContosoDevKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
     Registre el nombre de su almacén de claves.  
  
     La instrucción devuelve:  
  
    ```  
    Vault Name                       : ContosoDevKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoDevKeyVault  
    Vault URI: https://ContosoDevKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :   
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,   
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
4.  **Conceder permiso para que la entidad de servicio de Azure Active Directory acceda al Almacén de claves**  
  
     Puede autorizar a otros usuarios y aplicaciones a usar el Almacén de claves.   
    En este caso, vamos a usar la entidad de servicio de Azure Active Directory que creó en la Parte I para autorizar la instancia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!IMPORTANT]  
    >  La entidad de servicio de Azure Active Directory debe tener al menos los permisos `get`, `list`, `wrapKey`y `unwrapKey` para el almacén de claves.  
  
     Tal y como se muestra a continuación, use el **id. de cliente** de la Parte I para el parámetro `ServicePrincipalName` . El `Set-AzureRmKeyVaultAccessPolicy` se ejecuta en modo silencioso sin resultados si se ejecuta correctamente.  
  
    ```powershell  
    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoDevKeyVault'`  
      -ServicePrincipalName EF5C8E09-4D2A-4A76-9998-D93440D8115D `  
      -PermissionsToKeys get, list, wrapKey, unwrapKey  
    ```  
  
     Llame al cmdlet `Get-AzureRmKeyVault` para confirmar los permisos. En el resultado de la instrucción en "Directivas de acceso", debería aparecer el nombre de la aplicación de AAD como otro inquilino con acceso a este Almacén de claves.  
  
       
5.  **Generar una clave asimétrica en el Almacén de claves**  
  
     Hay dos maneras de generar una clave en Azure Key Vault: 1) Importar una clave existente o 2) Crear una nueva clave.  

    ### <a name="best-practice"></a>Procedimiento recomendado:
    
    Para garantizar una recuperación rápida de las claves y el acceso a los datos fuera de Azure, le recomendamos el siguiente proceso:
 
    1. Cree localmente la clave de cifrado en un dispositivo HSM local. (Asegúrese de que se trata de una clave RSA 2048 asimétrica, para que así se pueda almacenar en Azure Key Vault).
    2. Importe la clave de cifrado a Azure Key Vault. Consulte los pasos siguientes para saber cómo hacerlo.
    3. Antes de usar la clave por primera vez en Azure Key Vault, cree una copia de seguridad clave de Azure Key Vault. Obtenga más información sobre el comando [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) .
    4. Cada vez que se haga algún cambio en la clave (por ejemplo, que se agregue ACL, etiquetas o atributos clave), asegúrese de crear otra copia de seguridad clave de Azure Key Vault.

        > [!NOTE]  
        >  Crear una copia de seguridad de una clave es una operación clave de Azure Key Vault que devuelve un archivo que se puede guardar en cualquier lugar.

    ### <a name="types-of-keys"></a>Tipos de claves:
    Hay dos tipos de claves que se pueden generar en el Almacén de claves de Azure. Ambas son claves RSA de 2048 bits asimétricas.  
  
    -   **Protegida mediante software:** procesada en el software y cifrada en reposo. Las operaciones en claves protegidas mediante software se producen en las máquinas virtuales de Azure. Se recomienda para las claves que no se usan en una implementación de producción.  
  
    -   **Protegida por HSM:** creada y protegida por un módulo de seguridad de hardware (HSM) para disponer de seguridad adicional. El precio es de aproximadamente 1 $ por versión de clave.  
  
        > [!IMPORTANT]  
        >  El Conector de SQL Server requiere que el nombre de clave solo use los caracteres “a-z”, “A-Z”, “0-9” y “-“, con un límite de 26 caracteres.   
        > No funcionará el uso de diferentes versiones de claves bajo el mismo nombre de clave en el Almacén de claves de Azure con el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para sustituir una clave del Almacén de claves de Azure que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]usa, vea los pasos para sustituir una clave descritos en [Conector de SQL Server, apéndice](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)(Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;).  

    ### <a name="import-an-existing-key"></a>Importar una clave existente   
  
    Si dispone de una clave protegida mediante software RSA de 2048 bits existente, puede cargar la clave a Azure Key Vault. Por ejemplo, si guardó un archivo .PFX en la unidad `C:\\` en un archivo denominado `softkey.pfx` que desea cargar a Azure Key Vault, escriba lo siguiente para establecer la variable `securepfxpwd` para una contraseña de `12987553` para el archivo .PFX:  
  
    ``` powershell  
    $securepfxpwd = ConvertTo-SecureString –String '12987553' `  
      –AsPlainText –Force  
    ```  
  
    Después puede escribir lo siguiente para importar la clave desde el archivo .PFX, que protege la clave mediante software en el servicio de Key Vault (opción recomendada):  
  
    ``` powershell  
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
          -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
          -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
    ```  
 
    > [!IMPORTANT]  
    > En los escenarios de producción, le recomendamos encarecidamente que importe la clave asimétrica, porque permite al administrador custodiar la clave en un sistema de custodia de clave. Si la clave asimétrica se crea en el almacén, no se puede custodiar, porque la clave privada no puede salir nunca del almacén. Las claves que se usen para proteger datos críticos se deben custodiar. Si se pierde una clave asimétrica, los datos no podrán recuperarse nunca más.  

    ### <a name="create-a-new-key"></a>Crear una clave nueva

    ##### <a name="example"></a>Ejemplo:  
    Si lo desea, puede crear una nueva clave de cifrado directamente en Azure Key Vault y protegerla por software o por HSM. En este ejemplo crearemos una clave protegida por software con `Add-AzureKeyVaultKey cmdlet`:  

    ``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'ContosoRSAKey0' -Destination 'Software'  
    ```  
  
    La instrucción devuelve:  
  
    ```  
    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
    Key        :  {"kid":"https:contosodevKeyVault.azure.net/keys/  
                   ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
    VaultName  : contosodevkeyvault  
    Name       : contosoRSAKey0  
    Version    : <guid>  
    Id         : https://contosodevkeyvault.vault.azure.net:443/  
                 keys/ContosoRSAKey0/<guid>  
    ```  

    > [!IMPORTANT]  
    >  El Almacén de claves admite varias versiones de la clave con mismo nombre, pero las claves que use el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no deberían tener versiones y revertirse. Si el administrador quiere revertir la clave que se usa para el cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , debe crear una nueva clave con otro nombre en el almacén y usar la nueva clave para cifrar la clave de cifrado de datos (DEK).  
   
  
## <a name="part-iii-install-the-includessnoversionincludesssnoversion-mdmd-connector"></a>Parte III: Instalar el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Descargue el conector de SQL Server desde el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=521700). (Esto debe hacerlo el administrador del equipo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ).  

> [!NOTE]  
>  Las versiones 1.0.0.440 y anteriores se han reemplazado y ya no se admiten en entornos de producción. Actualice a la versión 1.0.1.0 o posterior visitando el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) y con las instrucciones de la sección "Actualización del conector de SQL Server" de la página [Conector de SQL Server, apéndice](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) .
  
 ![ekm-connector-install](../../../relational-databases/security/encryption/media/ekm-connector-install.png "ekm-connector-install")  
  
 El conector se instala de forma predeterminada en C:\Archivos de programa\Conector de SQL Server para Almacén de claves de Azure . Esta ubicación se puede cambiar durante la instalación. (Si la cambia, ajuste los siguientes scripts).  
  
 No hay ninguna interfaz para el conector, pero si está instalado correctamente, se instalará **Microsoft.AzureKeyVaultService.EKM.dll** en el equipo. Esta es la DLL del proveedor de servicios criptográficos EKM que se tiene que registrar con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con la instrucción `CREATE CRYPTOGRAPHIC PROVIDER` .  
  
 La instalación del conector de SQL Server también le permite descargar, si quiere, los scripts de muestra del cifrado de SQL Server.  
  
 Para ver las explicaciones de código de error, la configuración de mantenimiento o las tareas de mantenimiento para el conector de SQL Server, visite el apéndice que se encuentra en la parte inferior de este tema:  
  
-   [A. Instrucciones de mantenimiento para el conector de SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
  
-   [C. Explicaciones de código de error para el conector de SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="part-iv-configure-includessnoversionincludesssnoversion-mdmd"></a>Parte IV: Configurar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Diríjase a [B. Preguntas más frecuentes](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB) para ver una nota sobre los niveles de permisos mínimos necesarios para cada acción en esta sección.  
  
1.  **Inicie sqlcmd.exe o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio**  
  
2.  **Configurar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar EKM**  
  
     Ejecute el siguiente script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] para configurar [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para usar un proveedor EKM.  
  
    ```tsql  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
3.  **Registrar (crear) el Conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como proveedor EKM con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     Cree un proveedor de servicios criptográficos con el Conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , que es un proveedor EKM para el Almacén de claves de Azure.    
    Este ejemplo usa el nombre de `AzureKeyVault_EKM_Prov`.  
  
    ```tsql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
    > [!NOTE]  
    >  La ruta de acceso al archivo no puede tener una longitud superior a 256 caracteres.  
  
  
4.  **Configurar una credencial de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar el Almacén de claves**  
  
     Debe agregar una credencial a cada inicio de sesión que realice cifrado con una clave del Almacén de claves. Estas pueden incluir:  
  
    -   Un inicio de sesión de administrador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que vaya a usar el Almacén de claves para configurar y administrar los escenarios de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   Otros inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que pueden habilitar el cifrado de datos transparente TDE u otras características de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Hay una asignación de uno a uno entre credenciales e inicios de sesión. Es decir, cada inicio de sesión debe tener una credencial única.  
  
     Modifique el script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] siguiente como se indica a continuación:  
  
    -   Edite el argumento `IDENTITY` (`ContosoDevKeyVault`) para dirigirlo a Azure Key Vault.
        - Si usa **Azure público**, reemplace el argumento `IDENTITY` por el nombre de su Azure Key Vault de la parte II.
        - Si usa **nube pública de Azure** (por ejemplo, Azure Government, Azure China o Azure Germany), reemplace el argumento `IDENTITY` por el URI de almacén que se devolvió en la parte II, paso 3. No incluya "https://" en el URI de almacén.   
    -   Reemplace la primera parte del argumento `SECRET` con el **id. de cliente** de Azure de la parte I. En este ejemplo, el **id. de cliente** es `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  Debe quitar los guiones de **Client ID**.  
  
    -   Complete la segunda parte del argumento `SECRET` con el **secreto de cliente** de la parte I. En este ejemplo, el **secreto de cliente** de la parte I es `Replace-With-AAD-Client-Secret`. La cadena final para el argumento `SECRET` será una secuencia larga de letras y números, *sin guiones*.  
  
    ```tsql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     Para ver un ejemplo del uso de variables con los argumentos de **CREATE CREDENTIAL** y de cómo quitar mediante programación los guiones del id. de cliente, consulte [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md).  
  
5.  **Abra la clave del almacén de claves de Azure en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     Si ha importado una clave asimétrica como se ha descrito anteriormente en la Parte II, abra la clave proporcionando el nombre de esta en el siguiente script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Reemplace `CONTOSO_KEY` con el nombre que le gustaría tener en la clave de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    -   Reemplace `ContosoRSAKey0` con el nombre de la clave en el Almacén de claves de Azure.  
  
    ```tsql  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
## <a name="next-step"></a>Paso siguiente  
  
Ahora que ha completado la configuración básica, consulte cómo [Use SQL Server Connector con características de cifrado de SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)(Usar el conector de SQL Server con características de cifrado de SQL)   
  
## <a name="see-also"></a>Vea también  
 [Administración extensible de claves con el Almacén de claves de Azure](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
[Conector de SQL Server, apéndice](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  

