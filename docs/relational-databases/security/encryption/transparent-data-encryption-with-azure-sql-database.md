---
title: Cifrado de datos transparente con Azure SQL Database | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
- MSDN content
- MSDN - SQL DB
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TDE, SQL Database
- encryption (SQL Database), TDE
- Transparent Data Encryption, SQL Database
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c607015f1ead5b19d4c32c5bac62eb624b0578b
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Cifrado de datos transparente con Base de datos SQL de Azure
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx_md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] El cifrado de datos transparente le ayuda a protegerse frente a amenazas de actividad malintencionada mediante la realización de un cifrado y descifrado de la base de datos en tiempo real, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de realizar cambios en la aplicación.  
  
 TDE cifra el almacenamiento de una base de datos completa utilizando una clave simétrica denominada clave de cifrado de base de datos. En [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] la clave de cifrado de base de datos está protegida por un certificado de servidor integrado. El certificado de servidor integrado es único para cada servidor de [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] . Si una base de datos está en una relación de GeoDR, está protegido por una clave diferente en cada servidor. Si hay 2 bases de datos conectadas al mismo servidor, comparten el mismo certificado integrado. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] gira automáticamente estos certificados al menos cada 90 días. Para obtener una descripción general de TDE, vea [Cifrado de datos transparente &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md).  
  
 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] no admite la integración del Almacén de claves de Azure con TDE. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se ejecuta en una máquina virtual de Azure puede usar una clave asimétrica del almacén de claves. Para obtener más información, vea [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)llevar a cabo la administración de claves, que incluye una jerarquía de claves de cifrado y la copia de seguridad de las claves.  
  
##  <a name="Permissions"></a> Permisos  
 Para configurar TDE mediante el Portal de Azure, con la API de REST o con PowerShell, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL.  
  
 Para configurar TDE mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] se requiere lo siguiente:  
  
-   Para ejecutar la instrucción ALTER DATABASE con la opción SET es necesario ser miembro del rol **dbmanager** .  
  
##  <a name="Preview"></a> Habilitación de TDE en una base de datos mediante el Portal  
  
1.  Visite el Portal de Azure en la página [https://portal.azure.com](https://portal.azure.com) e inicie sesión con su cuenta de administrador de Azure o de colaborador.  
  
2.  En el encabezado de la izquierda, haga clic en a **EXAMINAR**y, a continuación, haga clic en **Bases de datos SQL**.  
  
3.  Con **Bases de datos SQL** seleccionado en el panel izquierdo, haga clic en la base de datos de usuario.  
  
4.  En la hoja de la base de datos, haga clic en **Toda la configuración**.  
  
5.  En la hoja **Configuración** , haga clic en la parte **Cifrado de datos transparente** para abrir la hoja **Cifrado de datos transparente** .  
  
6.  En la hoja **Cifrado de datos** , mueva el botón **Cifrado de datos** a la posición **Activado**y luego haga clic en **Guardar** (en la parte superior de la página) para aplicar la configuración. El **Estado de cifrado** aproximará el progreso del cifrado de datos transparente.  
  
     ![Cifrado de inicio TDE de base de datos SQL](../../../relational-databases/security/encryption/media/sqldb-tde-encrypt.png "Cifrado de inicio TDE de base de datos SQL")  
  
     También puede supervisar el progreso del cifrado mediante la conexión a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mediante una herramienta de consulta como [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] como un usuario de base de datos con el permiso **VER ESTADO DE LA BASE DE DATOS** . Consulte la columna **encryption_state** de la vista [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .  
  
##  <a name="Encrypt"></a> Habilitar TDE en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mediante Transact-SQL  
 Los pasos siguientes habilitan TDE.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  Conéctese a la base de datos mediante un inicio de sesión de administrador o de miembro del rol **dbmanager** de la base de datos maestra.  
  
2.  Ejecute las siguientes instrucciones para cifrar la base de datos.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  Para supervisar el progreso del cifrado en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], los usuarios de la base de datos que dispongan del permiso **VIEW DATABASE STATE** pueden consultar la columna **encryption_state** de la vista [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .  
  
##  <a name="EncryptPS"></a> Habilitación y deshabilitación de TDE en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mediante PowerShell  
 Mediante Azure PowerShell puede ejecutar el comando siguiente para activar/desactivar TDE. Es necesario conectar su cuenta a la ventana de PS antes de ejecutar el comando. Personalice el ejemplo para usar sus valores de los parámetros `ServerName`, `ResourceGroupName`y `DatabaseName` . Para obtener información adicional acerca de PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
> [!NOTE]  
>  Para continuar, debe instalar y configurar la versión 1.0 de Azure PowerShell. La versión 0.9.8 puede utilizarse, pero está en desuso y es preciso cambiar a los cmdlets AzureResourceManager utilizando el comando `PS C:\> Switch-AzureMode -Name AzureResourceManager` .  
  
###  <a name="PSlProcedure"></a>  
  
1.  Para habilitar TDE, devuelva el estado de TDE y visualice la actividad de cifrado.  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
    ```  
  
     Si utiliza la versión 0.9.8, use los comandos Set-AzureSqlDatabaseTransparentDataEncryption, Get-AzureSqlDatabaseTransparentDataEncryption, and Get-AzureSqlDatabaseTransparentDataEncryptionActivity.  
  
2.  Para deshabilitar TDE:  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    ```  
  
     Si utiliza la versión 0.9.8, use el comando Set-AzureSqlDatabaseTransparentDataEncryption.  
  
##  <a name="Decrypt"></a> Descifrado de una base de datos protegida por TDE en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>Para deshabilitar TDE mediante el portal de Azure  
  
1.  Visite el Portal de Azure en la página [https://portal.azure.com](https://portal.azure.com) e inicie sesión con su cuenta de administrador de Azure o de colaborador.  
  
2.  En el encabezado de la izquierda, haga clic en a **EXAMINAR**y, a continuación, haga clic en **Bases de datos SQL**.  
  
3.  Con **Bases de datos SQL** seleccionado en el panel izquierdo, haga clic en la base de datos de usuario.  
  
4.  En la hoja de la base de datos, haga clic en **Toda la configuración**.  
  
5.  En la hoja **Configuración** , haga clic en la parte **Cifrado de datos transparente** para abrir la hoja **Cifrado de datos transparente** .  
  
6.  En la hoja **Cifrado de datos transparente** , mueva el botón **Cifrado de datos** a la posición **Desactivado**y luego haga clic en **Guardar** (en la parte superior de la página) para aplicar la configuración. El **Estado de cifrado** aproximará el progreso del descifrado de datos transparente.  
  
     También puede supervisar el progreso del descifrado mediante la conexión a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mediante una herramienta de consulta como [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] como un usuario de base de datos con el permiso **VER ESTADO DE LA BASE DE DATOS** . Consulte la columna **encryption_state** de la vista [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>Para deshabilitar TDE mediante Transact-SQL  
  
1.  Conéctese a la base de datos mediante un inicio de sesión de administrador o de miembro del rol **dbmanager** de la base de datos maestra.  
  
2.  Ejecute las siguientes instrucciones para descifrar la base de datos.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  Para supervisar el progreso del cifrado en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], los usuarios de la base de datos que dispongan del permiso **VIEW DATABASE STATE** pueden consultar la columna **encryption_state** de la vista [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .  
  
##  <a name="Working"></a> Movimiento de una base de datos protegida de TDE en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
 No es necesario descifrar las bases de datos para las operaciones dentro de Azure. La configuración de TDE en la base de datos de origen o la base de datos principal se hereda de forma transparente en el destino. Aquí se incluyen operaciones que implican:  
  
-   Restauración geográfica  
  
-   Restauración a un momento dado de autoservicio  
  
-   Restaurar una base de datos eliminada  
  
-   Geo_Replication activa  
  
-   Creación de la copia de una base de datos  
  
 Cuando se exporta una base de datos protegida con TDE mediante la función Exportar base de datos del Portal de [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] o el Asistente para la importación y exportación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el contenido exportado de la base de datos no se cifra. Este contenido exportado se almacena en los archivos .bacpac no cifrados. Asegúrese de proteger adecuadamente los archivos .bacpac y de habilitar TDE una vez completada la importación de la nueva base de datos. 
 
 Por ejemplo, si el archivo .bacpac se exporta desde un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]local, el contenido importado de la base de datos nueva no se cifrará automáticamente. Del mismo modo, si el archivo .bacpac se exporta desde una [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]local, la base de datos nueva tampoco se cifra automáticamente.  
 
 La única excepción se produce cuando se exporta desde y hacia [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] : TDE se habilitará en la base de datos nueva, pero el archivo .bacpac mismo seguirá sin cifrarse.
  
## <a name="related-sql-server-topic"></a>Tema de SQL Server relacionado  
 [Habilitar TDE en SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>Vea también  
 [Cifrado de datos transparente &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
  

