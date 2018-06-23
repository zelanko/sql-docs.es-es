---
title: Cifrado de datos transparente con Azure SQL Database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TDE, SQL Database
- Transparent Data Encryption, SQL Database
- encryption (SQL Database) TDE
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1850458778cadbfe871880d42a7830c94078c2a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201872"
---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Cifrado de datos transparente con Base de datos SQL de Azure
  [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] cifrado de datos transparente (vista previa) le ayuda a protegerse contra la amenaza de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de la base de datos, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin requerir cambios en la aplicación.  
  
 TDE cifra el almacenamiento de una base de datos completa utilizando una clave simétrica denominada clave de cifrado de base de datos. En [!INCLUDE[ssSDS](../includes/sssds-md.md)] la clave de cifrado de base de datos está protegida por un certificado de servidor integrado. El certificado de servidor integrado es único para cada servidor de [!INCLUDE[ssSDS](../includes/sssds-md.md)] . Si una base de datos está en una relación de GeoDR, está protegido por una clave diferente en cada servidor. Si hay 2 bases de datos conectadas al mismo servidor, comparten el mismo certificado integrado. [!INCLUDE[msCoName](../includes/msconame-md.md)] gira automáticamente estos certificados al menos cada 90 días. Para obtener una descripción general de TDE, vea [Cifrado de datos transparente &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md).  
  
 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] no admite la integración del Almacén de claves de Azure con TDE. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se ejecuta en una máquina virtual de Azure puede usar una clave asimétrica del almacén de claves. Para obtener más información, consulte [ejemplo A: Transparent Data Encryption mediante el uso de una clave asimétrica desde el almacén de claves](../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md#ExampleA).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)] ([vista previa en algunas regiones](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
> [!IMPORTANT]  
>  Actualmente, se trata de una característica de vista previa. Reconoce y acepta que la implementación de [!INCLUDE[ssSDS](../includes/sssds-md.md)] cifrado de datos transparente en mis bases de datos está sujeta a los términos de vista previa en mi contrato de licencia (por ejemplo, el contrato Enterprise, contrato de Microsoft Azure o suscripción en línea de Microsoft Contrato), así como cualquier aplicable [términos de uso complementarios de Microsoft Azure Preview](http://azure.microsoft.com/support/legal/preview-supplemental-terms/).  
  
 La vista previa del estado de TDE se aplica incluso en el subconjunto de las regiones geográficas donde la familia de la versión V12 de [!INCLUDE[ssSDS](../includes/sssds-md.md)] se anuncia como con estado de disponibilidad general. TDE para [!INCLUDE[ssSDS](../includes/sssds-md.md)] no está diseñado para su uso en bases de datos de producción hasta que [!INCLUDE[msCoName](../includes/msconame-md.md)] anuncie que TDE se promueve de vista previa a disponibilidad general. Para más información sobre [!INCLUDE[ssSDS](../includes/sssds-md.md)] V12, consulte [Novedades de la base de datos de SQL Azure](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/).  
  
##  <a name="Permissions"></a> Permissions  
 Para inscriburse para obtener la vista previa y configurar TDE a través del portal de Azure, mediante la API de REST o mediante PowerShell, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL.  
  
 Para configurar TDE mediante [!INCLUDE[tsql](../includes/tsql-md.md)] se requiere lo siguiente:  
  
-   Debe estar ya registrado para la vista previa de TDE.  
  
-   Para crear la clave de cifrado de base de datos debe ser un [!INCLUDE[ssSDS](../includes/sssds-md.md)] administrador o debe ser un miembro de la **dbmanager** rol en el maestro de la base de datos y tener la **CONTROL** permiso en la base de datos.  
  
-   Para ejecutar la instrucción ALTER DATABASE con la opción SET solo se requiere la pertenencia al rol **dbmanager** .  
  
##  <a name="Preview"></a> Inscríbase en la vista previa de TDE y habilite TDE en una base de datos  
  
1.  Visite el Portal de Azure en [ https://portal.azure.com ](https://portal.azure.com) e inicie sesión con su cuenta de administrador de Azure o colaborador.  
  
2.  En el encabezado de la izquierda, haga clic en a **EXAMINAR**y, a continuación, haga clic en **Bases de datos SQL**.  
  
3.  Con **Bases de datos SQL** seleccionado en el panel izquierdo, haga clic en la base de datos de usuario.  
  
4.  En la hoja de la base de datos, haga clic en **Toda la configuración**.  
  
5.  En la hoja **Configuración** , haga clic en la parte **Cifrado de datos transparente (vista previa)** para abrir la hoja **VISTA PREVIA de cifrado de datos transparente** . Si todavía no está suscrito a la versión preliminar de TDE, se deshabilitará la configuración de cifrado de datos hasta que finalice el registro.  
  
6.  Haga clic en **TÉRMINOS DE LA VERSIÓN PRELIMINAR**.  
  
7.  Lea los términos de la vista previa y, si acepta los términos, seleccione la **términos de datos transparente encryptionPreview** casilla de verificación y, a continuación, haga clic en **Aceptar** cerca de la parte inferior de la página. Volver a la **datos encryptionPREVIEW** hoja, donde el **cifrado de datos** ahora debe habilitar el botón.  
  
8.  En la hoja **VERSIÓN PRELIMINAR de cifrado de datos** , mueva el botón **Cifrado de datos** a la posición **Activado**, y, a continuación, haga clic en **Guardar** (en la parte superior de la página) para aplicar la configuración. El **Estado de cifrado** aproximará el progreso del cifrado de datos transparente.  
  
     ![SQLDB_TDE_TermsNewUI](../../2014/database-engine/media/sqldb-tde-termsnewui.png "SQLDB_TDE_TermsNewUI")  
  
     También puede supervisar el progreso del cifrado mediante la conexión a [!INCLUDE[ssSDS](../includes/sssds-md.md)] mediante una herramienta de consulta como [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como un usuario de base de datos con el permiso **VER ESTADO DE LA BASE DE DATOS** . Consulta el `encryption_state` columna de la [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) vista.  
  
##  <a name="Encrypt"></a> Habilitar TDE en [!INCLUDE[ssSDS](../includes/sssds-md.md)] mediante Transact-SQL  
 En los pasos siguientes se supone que ya se ha registrado para la vista previa.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  Conéctese a la base de datos mediante un inicio de sesión de administrador o de miembro del rol **dbmanager** de la base de datos maestra.  
  
2.  Ejecute las siguientes instrucciones para crear una clave de cifrado de base de datos y cifrar la base de datos.  
  
    ```  
    -- Create the database encryption key that will be used for TDE.  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE ##MS_TdeCertificate##;  
  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  Para supervisar el progreso del cifrado en [!INCLUDE[ssSDS](../includes/sssds-md.md)], los usuarios con la base de datos la **VIEW DATABASE STATE** permiso puede consultar la `encryption_state` columna de la [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) vista.  
  
## <a name="enabling-tde-on-sql-database-by-using-powershell"></a>Habilitar TDE en SQL Database mediante PowerShell  
 Mediante Azure PowerShell puede ejecutar el comando siguiente para activar/desactivar TDE. Es necesario conectar su cuenta a la ventana de PS antes de ejecutar el comando. En los pasos siguientes se supone que ya se ha registrado para la vista previa. Para obtener información adicional acerca de PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
1.  Para habilitar TDE, devuelva el estado de TDE y visualice la actividad de cifrado.  
  
    ```  
    PS C:\> Switch-AzureMode -Name AzureResourceManager  
  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    ```  
  
2.  Para deshabilitar TDE:  
  
    ```  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    PS C:\> Switch-AzureMode -Name AzureServiceManagement  
    ```  
  
##  <a name="Decrypt"></a> Descifrado de una base de datos protegida por TDE en [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>Para deshabilitar TDE mediante Azure Portal  
  
1.  Visite el Portal de Azure en [ https://portal.azure.com ](https://portal.azure.com) e inicie sesión con su cuenta de administrador de Azure o colaborador.  
  
2.  En el encabezado de la izquierda, haga clic en a **EXAMINAR**y, a continuación, haga clic en **Bases de datos SQL**.  
  
3.  Con **Bases de datos SQL** seleccionado en el panel izquierdo, haga clic en la base de datos de usuario.  
  
4.  En la hoja de la base de datos, haga clic en **Toda la configuración**.  
  
5.  En la hoja **Configuración** , haga clic en la parte **Cifrado de datos transparente (vista previa)** para abrir la hoja **VISTA PREVIA de cifrado de datos transparente** .  
  
6.  En la hoja **VERSIÓN PRELIMINAR del cifrado de datos transparente** , mueva el botón **Cifrado de datos** a la posición **Desactivado**, y, a continuación, haga clic en **Guardar** (en la parte superior de la página) para aplicar la configuración. El **Estado de cifrado** aproximará el progreso del descifrado de datos transparente.  
  
     También puede supervisar el progreso del descifrado mediante la conexión a [!INCLUDE[ssSDS](../includes/sssds-md.md)] mediante una herramienta de consulta como [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] como un usuario de base de datos con el permiso **VER ESTADO DE LA BASE DE DATOS** . Consulta el `encryption_state` columna de la [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)vista.  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>Para deshabilitar TDE mediante Transact-SQL  
  
1.  Conéctese a la base de datos mediante un inicio de sesión de administrador o de miembro del rol **dbmanager** de la base de datos maestra.  
  
2.  Ejecute las siguientes instrucciones para descifrar la base de datos.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  Para supervisar el progreso del cifrado en [!INCLUDE[ssSDS](../includes/sssds-md.md)], los usuarios con la base de datos la **VIEW DATABASE STATE** permiso puede consultar la `encryption_state` columna de la [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) vista.  
  
##  <a name="Working"></a> Trabajar con TDE protegidas las bases de datos en [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
 No es necesario descifrar las bases de datos para las operaciones dentro de Azure. La configuración de TDE en la base de datos de origen o la base de datos principal se hereda de forma transparente en el destino. Aquí se incluyen operaciones que implican:  
  
-   Restauración geográfica  
  
-   Restauración a un momento dado de autoservicio  
  
-   Restaurar una base de datos eliminada  
  
-   Geo_Replication activa  
  
-   Creación de la copia de una base de datos  
  
##  <a name="Moving"></a> Mover una base de datos protegida de TDE mediante. Archivos Bacpac  
 Cuando se exporta un TDE protegida base de datos mediante la función Exportar base de datos en el [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] Portal o la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Import and Export Wizard, el contenido de la base de datos no está cifrada. El contenido se almacena en archivos .bacpac que no están cifrados.  Asegúrese de proteger adecuadamente los archivos .bacpac y de habilitar TDE una vez completada la importación de la nueva base de datos.  
  
## <a name="related-sql-server-topic"></a>Tema de SQL Server relacionado  
 [Habilitar TDE usando EKM](../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>Vea también  
 [Cifrado de datos transparente &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
