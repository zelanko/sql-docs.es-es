---
title: 'Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS | Microsoft Docs'
ms.custom: ''
ms.date: 10/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 5a8f0b9a18627da1e7d407b396686cb756ca5a4b
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2018
ms.locfileid: "48852117"
---
# <a name="tutorial-getting-started-with-always-encrypted-with-secure-enclaves-using-ssms"></a>Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial se explica cómo empezar a trabajar con los [enclaves seguros de Always Encrypted](encryption/always-encrypted-enclaves.md). En él encontrará:
- Cómo crear un entorno simple para probar y evaluar Always Encrypted con enclaves seguros.
- Cómo cifrar datos in situ y emitir consultas enriquecidas en columnas cifradas mediante SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Prerequisites

Para empezar a trabajar con Always Encrypted con enclaves seguros, necesita al menos dos equipos (pueden ser máquinas virtuales):

- El equipo con SQL Server para hospedar SQL Server y SSMS.
- El equipo HGS para ejecutar el servicio de protección de host, que es necesario para la atestación del enclave.

### <a name="sql-server-computer-requirements"></a>Requisitos del equipo con SQL Server

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] o posterior
- Windows 10 Enterprise versión 1809 o Windows Server 2019 Datacenter
- [SQL Server Management Studio (SSMS) 18.0 o versiones posteriores](../../ssms/download-sql-server-management-studio-ssms.md)

También puede instalar SSMS en otro equipo.

>[!WARNING] 
>En entornos de producción, no debe usar nunca SSMS ni otras herramientas para administrar las claves Always Encrypted, ni ejecutar consultas en datos cifrados en el equipo con SQL Server, ya que esto podría reducir o impedir la finalidad de utilizar Always Encrypted.

### <a name="hgs-computer-requirements"></a>Requisitos del equipo de HGS

- Windows Server 2019, edición Standard o Datacenter
- 2 CPU
- 8 GB de RAM
- 100 GB de almacenamiento

>[!NOTE]
>El equipo HGS no puede formar parte de un dominio antes de empezar.

## <a name="step-1-configure-the-hgs-computer"></a>Paso 1: Configurar el equipo HGS

En este paso, configurará el equipo HGS para ejecutar la atestación de la clave de host que admite el servicio de protección de host.

1. Inicie sesión en el equipo HGS como administrador (administrador local), abra una consola de Windows PowerShell con privilegios y agregue el rol del servicio de protección de host ejecutando el comando siguiente:

   ```powershell
   Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
   ```

2. Una vez reiniciado el equipo HGS, inicie sesión de nuevo con su cuenta de administrador, abra una consola de Windows PowerShell con privilegios y ejecute los comandos siguientes para instalar el servicio de protección de host y configurar su dominio. La contraseña que especifique aquí solo se aplicará a la contraseña del modo de reparación de servicios del directorio de Active Directory, pero no cambiará su contraseñas de inicio de sesión en la cuenta de administrador. Puede proporcionar el nombre de dominio que quiera para HgsDomainName.

   ```powershell
   $adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force
   Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
   ```

3. Después de que el equipo se reinicie de nuevo, inicie sesión con su cuenta de administrador (que ahora también es un administrador de dominio), abra una consola de Windows PowerShell con privilegios y configure la atestación de la clave de host para la instancia HGS. 

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey  
   ```

4. Ejecute el comando siguiente para obtener la dirección IP del equipo HGS. Guarde esta dirección IP para los pasos posteriores.

   ```powershell
   Get-NetIPAddress  
   ```

>[!NOTE]
>Como alternativa, si quiere hacer referencia a su equipo HGS con un nombre DNS, puede configurar un reenviador desde los servidores DNS corporativos para el nuevo controlador de dominio HGS.  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>Paso 2: Configurar el equipo con SQL Server como un host protegido
En este paso, deberá configurar el equipo con SQL Server como un host protegido registrado en HGS con una atestación de clave de host.
>[!NOTE]
>Solo se recomienda utilizar la atestación de clave de host para usarla en entornos de prueba. Debe usar la atestación de TPM para los entornos de producción.

1. Inicie sesión en el equipo con SQL Server como administrador, abra una consola de Windows PowerShell con privilegios e instale la característica de host protegido, que también instalará Hyper-V (si todavía no está instalado).

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

2. Reinicie el equipo con SQL Server cuando se le pida para completar la instalación de Hyper-V.
3. Recupere el valor de la siguiente variable para determinar el nombre del equipo con SQL Server.

   ```powershell
   $env:computername 
   ```

4. Vuelva a iniciar sesión en el equipo con SQL Server como un administrador, abra una consola de Windows PowerShell con privilegios, genere una clave de host única y exporte la clave pública resultante a un archivo.

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

5. Copie el archivo de clave de host generado en el paso anterior al equipo HGS. En las instrucciones siguientes se presupone que el nombre de archivo es hostkey.cer y que lo copia en el escritorio del equipo HGS.
6. En el equipo HGS, abra una consola de Windows PowerShell con privilegios y registre la clave de host del equipo con SQL Server con HGS:

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

7. En el equipo con SQL Server, ejecute el siguiente comando en una consola de Windows PowerShell con privilegios para indicar al equipo con SQL Server dónde debe hacer la atestación. Asegúrese de que indica la dirección IP o el nombre de DNS del equipo HGS. 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://<IP address or DNS name>/Attestation -KeyProtectionServerUrl http://<IP address or DNS name>/KeyProtection/  
   ```

El resultado del comando anterior debe mostrar que el estado de la atestación es correcto.

Si se produce un error HostUnreachable, significa que el equipo con SQL Server no puede comunicarse con HGS. Asegúrese de que se puede hacer ping al equipo HGS.

Un error UnauthorizedHost indica que la clave pública no se ha registrado con el servidor HGS. Repita los pasos 5 y 6 para resolver el error.

Si todo lo demás falla, ejecute Clear-HgsClientHostKey y repita los pasos del 4 al 7.

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>Paso 3: Configurar Always Encrypted con enclaves seguros en SQL Server

En este paso, deberá habilitar la funcionalidad de Always Encrypted usando enclaves en su instancia de SQL Server.

1. Abra SSMS, conéctese a la instancia de SQL Server como sysadmin y abra una nueva ventana de consulta.
2. Configure el tipo de enclave seguro a VBS.

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1
   RECONFIGURE
   ```

3. Reinicie su instancia de SQL Server para que se aplique el cambio anterior. Puede reiniciar la instancia en SSMS haciendo clic con el botón derecho en ella en el Explorador de objetos y seleccionando Reiniciar. Cuando se reinicie la instancia, vuelva a conectarse a ella.

4. Confirme que el enclave seguro se ha cargado ejecutando la siguiente consulta:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type'
   ```

    La consulta debería devolver una fila con un aspecto similar al siguiente:  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | tipo de enclave de cifrado de columnas | 1     | 1              |

5. Para habilitar los cálculos completos en columnas cifradas, ejecute la siguiente consulta:

   ```sql
   DBCC traceon(127,-1)
   ```

    > [!NOTE]
    > Los cálculos completos están deshabilitados de forma predeterminada en [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)]. Deben habilitarse mediante la instrucción anterior tras cada reinicio de la instancia de SQL Server.

## <a name="step-4-create-a-sample-database"></a>Paso 4: Crear una base de datos de ejemplo
En este paso, creará una base de datos con algunos datos de ejemplo, que cifrará más adelante.

1. Conéctese a su instancia de SQL Server usando SSMS.
2. Cree una base de datos denominada ContosoHR.

    ```sql
    CREATE DATABASE [ContosoHR] COLLATE Latin1_General_BIN2
    ```

3. Compruebe que esté conectado a la base de datos recién creada. Cree una tabla denominada Empleados.

    ```sql
    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY]
    GO
    ```

4. Agregue algunos registros de empleados a la tabla Empleados.

    ```sql
    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692)
    GO

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415)
    GO
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>Paso 5: Aprovisionar claves habilitadas para el enclave

En este paso, creará una clave de columna maestra y una clave de cifrado de columna que admiten los cálculos de enclave.

1. Conéctese a la base de datos mediante SSMS.
2. En el **Explorador de objetos**, expanda su base de datos y vaya a **Seguridad** > **Claves de Always Encrypted**.
3. Aprovisione una nueva clave maestra de columna habilitada para el enclave:
    1. Haga clic con el botón derecho en **Claves de Always Encrypted** y seleccione **Nueva clave maestra de columna…**
    2. Seleccione su nombre de clave maestra de columna: CMK1.
    3. Seleccione **Almacén de certificados de Windows (usuario actual o equipo local)** o **Azure Key Vault**.
    4. Seleccione **Permitir cálculos de enclave**.
    5. Si ha seleccionado Azure Key Vault, inicie sesión en Azure y seleccione su almacén de claves. Para obtener más información sobre cómo crear un almacén de claves para Always Encrypted, consulte [Administrar sus almacenes de claves desde Azure Portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/).
    6. Seleccione su clave si ya existe o siga las indicaciones incluidas en el formulario para crear una nueva clave.
    7. Seleccione **Aceptar**.

        ![Permitir cálculos de enclave](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)

4. Cree una nueva clave de cifrado de columnas habilitada para el enclave:

    1. Haga clic con el botón derecho en **Claves de Always Encrypted** y seleccione **Nueva clave maestra de columna**.
    2. Escriba un nombre para la nueva clave de cifrado de columnas: CEK1.
    3. En la lista desplegable **Clave maestra de columna**, seleccione la clave maestra de columna que creó en los pasos anteriores.
    4. Seleccione **Aceptar**.

## <a name="step-6-encrypt-some-columns-in-place"></a>Paso 6: Cifrar algunas columnas en su lugar

En este paso, va a cifrar los datos almacenados en las columnas SSN y Salario dentro del enclave del lado del servidor y después podrá probar una consulta SELECT de los datos.

1. En SSMS, configure una nueva ventana de consulta con la opción Always Encrypted habilitada para la conexión de base de datos.
    1. En SSMS, abra una nueva ventana de consulta.
    2. Haga clic con el botón derecho en la ventana de consulta nueva.
    3. Seleccione Conexión \> Cambiar conexión.
    4. Seleccione **Opciones**. Vaya a la pestaña **Always Encrypted**, seleccione **Habilitar Always Encrypted** y especifique su dirección URL de atestación de enclave.
    5. Seleccione **Conectar**.
2. En SSMS, configure otra ventana de consulta con la opción Always Encrypted deshabilitada para la conexión de base de datos.
    1. En SSMS, abra una nueva ventana de consulta.
    2. Haga clic con el botón derecho en la ventana de consulta nueva.
    3. Seleccione Conexión \> Cambiar conexión.
    4. Seleccione **Opciones**. Vaya a la pestaña **Always Encrypted**, asegúrese de que la opción **Habilitar Always Encrypted** no esté seleccionada.
    5. Seleccione **Conectar**.
3. Cifre las columnas SSN y Salario. En la ventana de consulta, con la opción Always Encrypted habilitada, pegue y ejecute las siguientes instrucciones:

    ```sql
    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11)
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON)
    GO
    DBCC FREEPROCCACHE
    GO

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON)
    GO
    DBCC FREEPROCCACHE
    GO
    ```

4. Para comprobar si las columnas SSN y Salario están cifradas, pegue la siguiente instrucción en la ventana de consulta y ejecútela con la opción Always Encrypted deshabilitada. La ventana de consulta debe devolver valores cifrados de las columnas SSN y Salario. Con la ventana de consulta habilitada para Always Encrypted, pruebe la misma consulta para ver los datos descifrados.

    ```sql
    SELECT * FROM [dbo].[Employees]
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>Paso 7: Ejecutar consultas completas sobre columnas cifradas

Ahora puede ejecutar consultas completas sobre columnas cifradas. Se realizará algún procesamiento de consulta dentro del enclave del lado del servidor. 

1. Habilite la parametrización para Always Encrypted.
    1. Seleccione **Consulta** en el menú principal de SSMS.
    2. Seleccione **Opciones de consulta…**.
    3. Vaya a **Ejecución** > **Avanzadas**.
    4. Seleccione o anule la selección de Habilitar parametrización de Always Encrypted.
    5. Seleccione Aceptar.
2. En la ventana de consulta, con la opción Always Encrypted habilitada, pegue y ejecute la siguiente consulta. La consulta debe devolver los valores de texto no cifrado y las filas que cumplan los criterios de búsqueda especificados.

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818'
    DECLARE @MinSalary [money] = $1000
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```

## <a name="next-steps"></a>Next Steps
Consulte [Configurar Always Encrypted con enclaves seguros](encryption/configure-always-encrypted-enclaves.md) para obtener ideas sobre otros casos de uso. También puede intentar lo siguiente:

- [Configurar la atestación de TPM.](https://docs.microsoft.com/en-us/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode)
- [Configurar HTTPS para la instancia HGS.](https://docs.microsoft.com/en-us/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https)
- Desarrollar aplicaciones que emitan consultas completas sobre columnas cifradas.
