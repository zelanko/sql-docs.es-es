---
title: Administración extensible de claves con Azure Key Vault (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault
- TDE, EKM and key vault
- Extensible Key Management with key vault
- Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: c2a6acd93bc711e4722f3ca437b17cba603dfcad
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372767"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Administración extensible de claves con Azure Key Vault (SQL Server)
  El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conector para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Key Vault permite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cifrado para aprovechar el servicio de Azure Key Vault como un [administración Extensible de claves &#40;EKM&#41; ](extensible-key-management-ekm.md) proveedor para proteger su claves de cifrado.  
  
 Este tema incluye:  
  
-   [Usos de EKM](#Uses)  
  
-   [Paso 1: Configuración de Key Vault para su uso con SQL Server](#Step1)  
  
-   [Paso 2: Instalación del conector SQL Server](#Step2)  
  
-   [Paso 3: Configurar SQL Server para usar un proveedor EKM para Key Vault](#Step3)  
  
-   [Ejemplo A: Cifrado de datos transparente mediante el uso de una clave asimétrica desde el almacén de claves](#ExampleA)  
  
-   [Ejemplo B: Cifrado de copias de seguridad con una clave asimétrica desde el almacén de claves](#ExampleB)  
  
-   [Ejemplo C: Cifrado de nivel de columna mediante el uso de una clave asimétrica desde el almacén de claves](#ExampleC)  
  
##  <a name="Uses"></a> Usos de EKM  
 Una organización puede utilizar el cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para proteger datos confidenciales. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluye cifrado [cifrado de datos transparente &#40;TDE&#41;](transparent-data-encryption.md), [cifrado de nivel de columna](/sql/t-sql/functions/cryptographic-functions-transact-sql) (CLE) y [cifrado de copia de seguridad](../../backup-restore/backup-encryption.md). En todos estos casos, los datos se cifran con una clave de cifrado de datos simétrica. La clave de cifrado de datos simétrica se protege, además, cifrándose con una jerarquía de claves almacenadas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O bien, la arquitectura del proveedor EKM permite a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proteger las claves de cifrado de datos con una clave asimétrica que se almacena fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en un proveedor de servicios criptográficos externo. El uso de la arquitectura de proveedor de EKM agrega un nivel de seguridad adicional y permite a las organizaciones separar la administración de claves y datos.  
  
 El conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de Azure Key Vault permite a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usar el servicio de almacén de claves de alto rendimiento, alta disponibilidad y escalable como un proveedor de EKM para la protección de claves de cifrado. El servicio de almacén de claves se puede usar con instalaciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en máquinas virtuales de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure y para servidores locales. El servicio Almacén de claves también permite usar módulos de seguridad de hardware (HSM) supervisados y controlados estrechamente. Así, se obtiene un mayor grado de protección para las claves de cifrado asimétricas. Para obtener más información sobre el Almacén de claves, consulte el tema sobre el [Almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521401).  
  
 La siguiente imagen resume el flujo de procesos de EKM usando el almacén de claves. Los números de pasos del proceso de la imagen no de proceso de la imagen no se ofrecen con el fin de que coincidan con los números de los pasos de configuración que siguen a la imagen.  
  
 ![Administración extensible de claves de SQL mediante Azure Key Vault](../../../database-engine/media/ekm-using-azure-key-vault.png "Administración extensible de claves de SQL mediante Azure Key Vault")  
  
##  <a name="Step1"></a> Paso 1: Configuración de Key Vault para su uso con SQL Server  
 Siga estos pasos para configurar un Almacén de claves y poder usarlo con [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] para la protección de claves de cifrado. Puede que la organización ya use un almacén. Si no existe un almacén, el administrador de Azure de su organización encargado de administrar las claves de cifrado puede crear uno, generar una clave asimétrica en él y, a continuación, autorizar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a usar la clave. Para familiarizarse con la revisión del servicio de almacén de claves, consulte [Introducción al almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521402)y la referencia sobre [cmdlets del almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521403) de PowerShell.  
  
> [!IMPORTANT]  
>  Si tiene varias suscripciones de Azure, debe usar la suscripción que contenga [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
1.  **Crear un almacén:** Crear un almacén siguiendo las instrucciones en el **crear un almacén de claves** sección de [empezar a trabajar con Azure Key Vault](https://go.microsoft.com/fwlink/?LinkId=521402). Registre el nombre del almacén. En este tema, se usa **ContosoKeyVault** como nombre del Almacén de claves.  
  
2.  **Generar una clave asimétrica en el almacén:** La clave asimétrica en el Almacén de claves se usa para proteger las claves de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La parte pública de la clave asimétrica es la única que sale del almacén: el almacén no exporta nunca la parte privada. Todas las operaciones de cifrado en las que se usa la clave asimétrica se delegan al Almacén de claves de Azure y están protegidas por la seguridad del Almacén de claves.  
  
     Hay varias maneras distintas de generar una clave asimétrica y almacenarla en el almacén. Puede crear una clave de forma externa e importarla al almacén como un archivo.pfx. También puede crear la clave directamente en el almacén mediante las API de almacén de claves.  
  
     El conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere que las claves asimétricas sean RSA de 2.048 bits y el nombre de la clave solo puede contener los caracteres “a-z”, “A-z”, “0-9” y “-”. En este documento, el nombre de la clave asimétrica es **ContosoMasterKey**. Reemplace este nombre por el nombre único que utilice para la clave.  
  
    > [!IMPORTANT]  
    >  En los escenarios de producción, le recomendamos encarecidamente que importe la clave asimétrica, porque permite al administrador custodiar la clave en un sistema de custodia de clave. Si la clave asimétrica se crea en el almacén, no se puede custodiar, porque la clave privada no puede salir nunca del almacén. Las claves que se usen para proteger datos críticos se deben custodiar. Si se pierde una clave asimétrica, los datos no podrán recuperarse nunca más.  
  
    > [!IMPORTANT]  
    >  El Almacén de claves admite varias versiones de la clave que tengan el mismo nombre. Las claves que use el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no deben tener versiones ni revertirse. Si el administrador quiere revertir la clave que se usa para el cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , debe crear una nueva clave con otro nombre en el almacén y utilizar la nueva clave para cifrar la clave de cifrado de datos (DEK).  
  
     Para más información sobre cómo importar una clave en el Almacén de claves o crear una clave en el Almacén de claves (no recomendado en entornos de producción), consulte la sección sobre **cómo agregar una clave o un secreto al Almacén de claves** de la [introducción al Almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521402).  
  
3.  **Obtenga Azure Active Directory las entidades de servicio que se usará para SQL Server:** Cuando la organización se suscribe a un servicio en la nube de Microsoft, obtiene un Azure Active Directory. Cree **entidades de servicio** en Azure Active Directory para que las use [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (para autenticarse a sí mismo en Azure Active Directory) al acceder al Almacén de claves.  
  
    -   Una **entidad de servicio** será necesaria para que un administrador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acceda al almacén mientras configura [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que use el cifrado.  
  
    -   Otra **entidad de servicio** será necesaria para que [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] acceda al almacén y pueda desempaquetar las claves utilizadas en el cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Para más información sobre cómo registrar una aplicación y generar una entidad de servicio, consulte la sección sobre **cómo registrar una aplicación con Azure Active Directory** en la [introducción al Almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521402). El proceso de registro devuelve un **Id. de aplicación** (también llamado **Id. de cliente**) y una **clave de autenticación** (también llamada **secreto**) para cada **entidad de servicio**de Azure Active Directory. Cuando se usa en el `CREATE CREDENTIAL` instrucción, debe quitar el guión de la **Id. de cliente**. Regístrelos para usarlos en los siguientes scripts:  
  
    -   **Entidad de servicio** para un **sysadmin** inicio de sesión: **CLIENTID_sysadmin_login** y **SECRET_sysadmin_login**  
  
    -   **Entidad de servicio** para el [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine** y **SECRET_DBEngine**.  
  
4.  **Conceda permiso a las entidades de servicio tener acceso a Key Vault:** Tanto el **CLIENTID_sysadmin_login** y **CLIENTID_DBEngineService entidades** requieren el **obtener**, **lista**,  **wrapKey**, y **unwrapKey** permisos en el almacén de claves. Si tiene pensado crear las claves con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , también deberá conceder el permiso **create** en el Almacén de claves.  
  
    > [!IMPORTANT]  
    >  Los usuarios deben habilitar, al menos, las operaciones **wrapKey** y **unwrapKey** para el almacén de claves.  
  
     Para más información sobre cómo conceder permisos en el almacén, consulte la sección sobre **cómo autorizar a la aplicación para que use la clave o el secreto** de la [introducción al Almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521402).  
  
     Vínculos a documentación del Almacén de claves de Azure  
  
    -   [¿Qué es el Almacén de claves de Azure?](https://go.microsoft.com/fwlink/?LinkId=521401)  
  
    -   [Introducción al Almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521402)  
  
    -   Referencia de [cmdlets del Almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521403) de PowerShell  
  
##  <a name="Step2"></a> Paso 2: Instalar el conector de SQL Server  
 El administrador del equipo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] descarga e instala el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . El conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se puede descargar desde el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=521700).  Busque el **conector de SQL Server para el Almacén de claves de Microsoft Azure**, revise los detalles, los requisitos del sistema y las instrucciones de instalación y elija la opción de descargar el conector e iniciar la instalación con **Ejecutar**. Revise la licencia, acéptela y continúe.  
  
 De forma predeterminada, el conector se instala en **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**. Esta ubicación se puede cambiar durante la instalación. (Si la cambia, ajuste los siguientes scripts).  
  
 Al finalizar la instalación, estarán instalados en el equipo:  
  
-   **Microsoft.AzureKeyVaultService.EKM.dll**: es la DLL del proveedor de servicios criptográficos EKM que se tiene que registrar con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con la instrucción CREATE CRYPTOGRAPHIC PROVIDER.  
  
-   **Conector de SQL Server de Azure Key Vault**: es un servicio de Windows que permite al proveedor de servicios criptográficos EKM comunicarse con el Almacén de claves.  
  
 La instalación del conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] también le permite descargar, si quiere, los scripts de muestra del cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="Step3"></a> Paso 3: configuración de SQL Server para usar un proveedor EKM para Key Vault  
  
###  <a name="Permissions"></a> Permissions  
 Para completar este proceso, son necesarios el permiso CONTROL SERVER o la pertenencia al rol fijo de servidor **sysadmin** . Los siguientes permisos son necesarios para realizar acciones concretas:  
  
-   Para crear un proveedor de servicios criptográficos, son necesarios el permiso CONTROL SERVER o la pertenencia al rol fijo de servidor **sysadmin** .  
  
-   Para cambiar una opción de configuración y ejecutar la instrucción RECONFIGURE, debe tener el permiso ALTER SETTINGS de nivel de servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
-   Para crear una credencial, es necesario el permiso ALTER ANY CREDENTIAL.  
  
-   Para agregar una credencial a un inicio de sesión, es necesario el permiso ALTER ANY LOGIN.  
  
-   Para crear una clave asimétrica, es necesario el permiso CREATE ASYMMETRIC KEY.  
  
###  <a name="TsqlProcedure"></a> Para configurar SQL Server para usar un proveedor de servicios criptográficos  
  
1.  Configure [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para utilizar EKM y registre (cree) el proveedor de servicios criptográficos con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    ```  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
  
    -- Create a cryptographic provider, using the SQL Server Connector  
    -- which is an EKM provider for the Azure Key Vault. This example uses   
    -- the name AzureKeyVault_EKM_Prov.  
  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO   
    ```  
  
2.  Configure una credencial de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para un inicio de sesión de administrador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , para utilizar el Almacén de claves con el fin de configurar y administrar escenarios de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!IMPORTANT]  
    >  El **identidad** argumento de `CREATE CREDENTIAL` requiere el nombre del almacén de claves. El **secreto** argumento de `CREATE CREDENTIAL` requiere la  *\<Id. de cliente >* (sin guiones) y  *\<secreto >* pasarse sin un espacio entre ellos.  
  
     En el ejemplo siguiente, el **Id. de cliente** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) se deja sin guiones y se introduce como la cadena `EF5C8E094D2A4A769998D93440D8115D` . El **secreto** se representa con la cadena *SECRET_sysadmin_login*.  
  
    ```  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
  
    -- Add the credential to the SQL Server administrators domain login   
    ALTER LOGIN [<domain>/<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     Para obtener un ejemplo del uso de variables para el `CREATE CREDENTIAL` argumentos y cómo quitar mediante programación los guiones del identificador de cliente, consulte [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql).  
  
3.  Si importó una clave asimétrica como se describió anteriormente en el paso 1, sección 3, abra la clave proporcionando el nombre de la clave en el ejemplo siguiente.  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
  
     Aunque no se recomienda para la producción (porque no se puede exportar la clave), es posible crear una clave asimétrica directamente en el almacén de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no importó una clave anteriormente, cree una clave asimétrica en el Almacén de claves para realizar pruebas con el siguiente script. Ejecute el script con un inicio de sesión aprovisionado con la credencial **sysadmin_ekm_cred** .  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH ALGORITHM = RSA_2048,  
    PROVIDER_KEY_NAME = 'ContosoMasterKey';  
    ```  
  
> [!TIP]  
>  Los usuarios que reciben el error **no se puede exportar la clave pública del proveedor. Código de error de proveedor: 2053.** debe comprobar sus permisos **get**, **list**, **wrapKey**y **unwrapKey** en el almacén de claves.  
  
 Para obtener más información, vea:  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
## <a name="examples"></a>Ejemplos  
  
###  <a name="ExampleA"></a> Ejemplo A: cifrado de datos transparente con una clave asimétrica desde Key Vault  
 Después de completar los pasos anteriores, cree una credencial y un inicio de sesión y cree una clave de cifrado de base de datos protegida por la clave asimétrica en el Almacén de claves. Use la clave de cifrado de base de datos para cifrar una base de datos con cifrado de datos transparente (TDE).  
  
 Para cifrar una base de datos, es necesario tener el permiso CONTROL en la base de datos.  
  
##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>Para habilitar TDE con EKM y el Almacén de claves  
  
1.  Cree una credencial de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que la use [!INCLUDE[ssDE](../../../includes/ssde-md.md)] al acceder al Almacén de claves EKM mientras se carga la base de datos.  
  
    > [!IMPORTANT]  
    >  El **identidad** argumento de `CREATE CREDENTIAL` requiere el nombre del almacén de claves. El **secreto** argumento de `CREATE CREDENTIAL` requiere la  *\<Id. de cliente >* (sin guiones) y  *\<secreto >* pasarse sin un espacio entre ellos.  
  
     En el ejemplo siguiente, el **Id. de cliente** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) se deja sin guiones y se introduce como la cadena `EF5C8E094D2A4A769998D93440D8115D` . El **secreto** se representa con la cadena *SECRET_DBEngine*.  
  
    ```  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
    ```  
  
2.  Cree un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que lo use [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para TDE y agréguele la credencial. En este ejemplo, se utiliza la clave asimétrica CONTOSO_KEY almacenada en el Almacén de claves, que se importó o se creó anteriormente para la base de datos maestra, como se describe en el [paso 3, sección 3](#Step3) , más arriba.  
  
    ```  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  Cree la clave de cifrado de base de datos (DEK) que se utilizará para TDE. La DEK puede crearse con cualquier algoritmo compatible con SQL Server y cualquier longitud de clave. La DEK estará protegida por la clave asimétrica en el Almacén de claves.  
  
     En este ejemplo, se utiliza la clave asimétrica CONTOSO_KEY almacenada en el Almacén de claves, que se importó o se creó anteriormente, como se describe en el [paso 3, sección 3](#Step3) , más arriba.  
  
    ```  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_128   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
     Para obtener más información, vea:  
  
    -   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
    -   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
###  <a name="ExampleB"></a> Ejemplo B: Cifrado de copias de seguridad con una clave asimétrica desde Key Vault  
 Las copias de seguridad cifradas se admiten a partir de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. En el ejemplo siguiente, se crea y se restaura una copia de seguridad cifrada con una clave de cifrado de datos protegida por la clave asimétrica en el Almacén de claves.  
  
```  
USE master;  
BACKUP DATABASE [DATABASE_TO_BACKUP]  
TO DISK = N'[PATH TO BACKUP FILE]'   
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);  
GO  
```  
  
 Código de muestra de la restauración.  
  
```  
RESTORE DATABASE [DATABASE_TO_BACKUP]  
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;  
GO  
```  
  
 Para obtener más información sobre las opciones de copia de seguridad, consulte [copia de seguridad &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
###  <a name="ExampleC"></a> Ejemplo C: Cifrado de nivel de columna con una clave asimétrica desde el Almacén de claves  
 En el ejemplo siguiente, se crea una clave simétrica protegida por la clave asimétrica en el Almacén de claves. Luego, se utiliza la clave simétrica para cifrar los datos de la base de datos.  
  
 En este ejemplo, se utiliza la clave asimétrica CONTOSO_KEY almacenada en el Almacén de claves, que se importó o se creó anteriormente, como se describe en el [paso 3, sección 3](#Step3) , más arriba. Para utilizar esta clave asimétrica en la base de datos `ContosoDatabase` , debe ejecutar de nuevo la instrucción CREATE ASYMMETRIC KEY para proporcionar a la base de datos `ContosoDatabase` una referencia a la clave.  
  
```  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [Administración extensible de claves &#40;EKM&#41;](extensible-key-management-ekm.md)   
 [Habilitar TDE con EKM](enable-tde-on-sql-server-using-ekm.md)   
 [Cifrado de copia de seguridad](../../backup-restore/backup-encryption.md)   
 [Crear una copia de seguridad cifrada](../../backup-restore/create-an-encrypted-backup.md)  
  
  
