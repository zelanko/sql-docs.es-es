---
title: Cifrado de datos transparente con Azure SQL Database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TDE, SQL Database
- Transparent Data Encryption, SQL Database
- encryption (SQL Database) TDE
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cc1dd416f5efb1404d107f1b55988ae0be68f0ce
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798074"
---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Cifrado de datos transparente con Azure SQL Database
  [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] cifrado de datos transparente (vista previa) le ayuda a protegerse contra la amenaza de la actividad malintencionada realizando un cifrado y descifrado en tiempo real, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin requerir cambios en la aplicación.  
  
 TDE cifra el almacenamiento de una base de datos completa utilizando una clave simétrica denominada clave de cifrado de base de datos. En [!INCLUDE[ssSDS](../includes/sssds-md.md)] la clave de cifrado de base de datos está protegida por un certificado de servidor integrado. El certificado de servidor integrado es único para cada servidor [!INCLUDE[ssSDS](../includes/sssds-md.md)] . Si una base de datos está en una relación de GeoDR, está protegido por una clave diferente en cada servidor. Si hay 2 bases de datos conectadas al mismo servidor, comparten el mismo certificado integrado. [!INCLUDE[msCoName](../includes/msconame-md.md)] gira automáticamente estos certificados al menos cada 90 días. Para obtener una descripción general de TDE, vea [Cifrado de datos transparente &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md).  
  
 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] no admite la integración de Azure Key Vault con TDE. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se ejecuta en una máquina virtual de Azure puede usar una clave asimétrica de Key Vault. Para obtener más información, vea [Example A: Transparent Data Encryption by Using an Asymmetric Key from the Key Vault](../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md#ExampleA).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)] ([vista previa en algunas regiones](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
> [!IMPORTANT]  
>  Actualmente, se trata de una característica de vista previa. Reconoce y acepta que la implementación del cifrado de datos transparente de [!INCLUDE[ssSDS](../includes/sssds-md.md)] en mis bases de datos está sujeta a los términos de vista previa del contrato de licencia (por ejemplo, el contrato Enterprise, contrato de Microsoft Azure o el contrato Microsoft Online Subscription), así como cualquier [término complementario de vista previa de Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)aplicable.  
  
 La vista previa del estado de TDE se aplica incluso en el subconjunto de las regiones geográficas donde la familia de la versión V12 de [!INCLUDE[ssSDS](../includes/sssds-md.md)] se anuncia como con estado de disponibilidad general. TDE para [!INCLUDE[ssSDS](../includes/sssds-md.md)] no está diseñado para su uso en bases de datos de producción hasta que [!INCLUDE[msCoName](../includes/msconame-md.md)] anuncie que TDE se promueve de vista previa a disponibilidad general. Para más información sobre [!INCLUDE[ssSDS](../includes/sssds-md.md)] V12, consulte [Novedades de la base de datos de SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/).  
  
##  <a name="Permissions"></a> Permisos  
 Para inscriburse para obtener la vista previa y configurar TDE a través del portal de Azure, mediante la API de REST o mediante PowerShell, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL.  
  
 Para configurar TDE mediante [!INCLUDE[tsql](../includes/tsql-md.md)] se requiere lo siguiente:  
  
-   Debe estar ya registrado para la vista previa de TDE.  
  
-   Para crear la clave de cifrado de la base de datos debe ser un administrador de [!INCLUDE[ssSDS](../includes/sssds-md.md)] o debe ser miembro del rol **dbmanager** en la base de datos maestra y tener el permiso **CONTROL** en la base de datos.  
  
-   Para ejecutar la instrucción ALTER DATABASE con la opción SET solo se requiere la pertenencia al rol **dbmanager** .  
  
##  <a name="Preview"></a>Suscríbase a la versión preliminar de TDE y habilite TDE en una base de datos  
  
1.  Visite Azure portal en [https://portal.azure.com](https://portal.azure.com) e inicie sesión con su cuenta de administrador o colaborador de Azure.  
  
2.  En el encabezado de la izquierda, haga clic en a **EXAMINAR**y, a continuación, haga clic en **Bases de datos SQL**.  
  
3.  Con **Bases de datos SQL** seleccionado en el panel izquierdo, haga clic en la base de datos de usuario.  
  
4.  En la hoja de la base de datos, haga clic en **Toda la configuración**.  
  
5.  En la hoja **Configuración** , haga clic en la parte **Cifrado de datos transparente (vista previa)** para abrir la hoja **VISTA PREVIA de cifrado de datos transparente** . Si todavía no está suscrito a la versión preliminar de TDE, se deshabilitará la configuración de cifrado de datos hasta que finalice el registro.  
  
6.  Haga clic en **TÉRMINOS DE LA VERSIÓN PRELIMINAR**.  
  
7.  Lea los términos de la versión preliminar y, si está de acuerdo con los términos, active la casilla de **EncryptionPreview datos transparentes** y, a continuación, haga clic en **Aceptar** cerca de la parte inferior de la página. Volver a la hoja **Data encryptionPREVIEW** , donde ahora debe estar habilitado el botón de **cifrado de datos** .  
  
8.  En la hoja **VERSIÓN PRELIMINAR de cifrado de datos** , mueva el botón **Cifrado de datos** a la posición **Activado**, y, a continuación, haga clic en **Guardar** (en la parte superior de la página) para aplicar la configuración. El **Estado de cifrado** aproximará el progreso del cifrado de datos transparente.  
  
     ![SQLDB_TDE_TermsNewUI](../../2014/database-engine/media/sqldb-tde-termsnewui.png "SQLDB_TDE_TermsNewUI")  
  
     También puede supervisar el progreso del cifrado mediante la conexión a [!INCLUDE[ssSDS](../includes/sssds-md.md)] mediante una herramienta de consulta como [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como un usuario de base de datos con el permiso **VER ESTADO DE LA BASE DE DATOS** . Consulte la columna `encryption_state` de la vista [Sys. dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) .  
  
##  <a name="Encrypt"></a> Habilitar TDE en [!INCLUDE[ssSDS](../includes/sssds-md.md)] mediante Transact-SQL  
 En los pasos siguientes se supone que ya se ha registrado para la vista previa.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  Conéctese a la base de datos mediante un inicio de sesión de administrador o de miembro del rol **dbmanager** de la base de datos maestra.  
  
2.  Ejecute las siguientes instrucciones para crear una clave de cifrado de base de datos y cifrar la base de datos.  
  
    ```sql
    -- Create the database encryption key that will be used for TDE.  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE ##MS_TdeCertificate##;  
  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  Para supervisar el progreso del cifrado en [!INCLUDE[ssSDS](../includes/sssds-md.md)], los usuarios de la base de datos con el permiso **View Database State** pueden consultar la columna `encryption_state` de la vista [Sys. dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) .  
  
## <a name="enabling-tde-on-sql-database-by-using-powershell"></a>Habilitar TDE en la base de datos SQL mediante PowerShell  
 Mediante Azure PowerShell puede ejecutar el comando siguiente para activar/desactivar TDE. Es necesario conectar su cuenta a la ventana de PS antes de ejecutar el comando. En los pasos siguientes se supone que ya se ha registrado para la vista previa. Para obtener información adicional acerca de PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
1.  Para habilitar TDE, devuelva el estado de TDE y visualice la actividad de cifrado.  
  
    ```powershell
    Switch-AzureMode -Name AzureResourceManager
    Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    Get-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
    Get-AzureSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"
    ```  
  
2.  Para deshabilitar TDE:  
  
    ```powershell
    Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
    Switch-AzureMode -Name AzureServiceManagement  
    ```  
  
##  <a name="Decrypt"></a> Descifrado de una base de datos protegida por TDE en [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>Para deshabilitar TDE mediante el portal de Azure  
  
1.  Visite Azure portal en [https://portal.azure.com](https://portal.azure.com) e inicie sesión con su cuenta de administrador o colaborador de Azure.  
  
2.  En el encabezado de la izquierda, haga clic en a **EXAMINAR**y, a continuación, haga clic en **Bases de datos SQL**.  
  
3.  Con **Bases de datos SQL** seleccionado en el panel izquierdo, haga clic en la base de datos de usuario.  
  
4.  En la hoja de la base de datos, haga clic en **Toda la configuración**.  
  
5.  En la hoja **Configuración** , haga clic en la parte **Cifrado de datos transparente (vista previa)** para abrir la hoja **VISTA PREVIA de cifrado de datos transparente** .  
  
6.  En la hoja **VERSIÓN PRELIMINAR del cifrado de datos transparente** , mueva el botón **Cifrado de datos** a la posición **Desactivado**, y, a continuación, haga clic en **Guardar** (en la parte superior de la página) para aplicar la configuración. El **Estado de cifrado** aproximará el progreso del descifrado de datos transparente.  
  
     También puede supervisar el progreso del descifrado mediante la conexión a [!INCLUDE[ssSDS](../includes/sssds-md.md)] mediante una herramienta de consulta como [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] como un usuario de base de datos con el permiso **VER ESTADO DE LA BASE DE DATOS** . Consulte la columna `encryption_state` de la vista [Sys. dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql).  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>Para deshabilitar TDE mediante Transact-SQL  
  
1.  Conéctese a la base de datos mediante un inicio de sesión de administrador o de miembro del rol **dbmanager** de la base de datos maestra.  
  
2.  Ejecute las siguientes instrucciones para descifrar la base de datos.  
  
    ```sql
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  Para supervisar el progreso del cifrado en [!INCLUDE[ssSDS](../includes/sssds-md.md)], los usuarios de la base de datos con el permiso **View Database State** pueden consultar la columna `encryption_state` de la vista [Sys. dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) .  
  
##  <a name="Working"></a>Trabajar con bases de datos protegidas por TDE en [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
 No es necesario descifrar las bases de datos para las operaciones dentro de Azure. La configuración de TDE en la base de datos de origen o la base de datos principal se hereda de forma transparente en el destino. Aquí se incluyen operaciones que implican:  
  
-   Restauración geográfica  
  
-   Restauración a un momento dado de autoservicio  
  
-   Restaurar una base de datos eliminada  
  
-   Geo_Replication activa  
  
-   Creación de la copia de una base de datos  
  
##  <a name="Moving"></a>Mover una base de datos protegida por TDE al usar. Archivos BacPac  
 Cuando se exporta una base de datos protegida mediante TDE mediante la función Exportar base de datos del portal de [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] o el asistente para la exportación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , el contenido de la base de datos no se cifra. El contenido se almacena en archivos .bacpac que no están cifrados.  Asegúrese de proteger adecuadamente los archivos .bacpac y de habilitar TDE una vez completada la importación de la nueva base de datos.  
  
## <a name="related-sql-server-topic"></a>Tema de SQL Server relacionado  
 [Habilitar TDE con EKM](../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>Vea también  
 [Cifrado de datos transparente &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
