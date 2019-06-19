---
title: Administrar una base de datos del servidor de informes (Modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- renaming databases
- report server database
- databases [Reporting Services], administering
- reportservertempdb
- reportserver database
ms.assetid: 97b2e1b5-3869-4766-97b9-9bf206b52262
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d155437880f1fb93779a2352bd507ea83de16256
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104280"
---
# <a name="administer-a-report-server-database-ssrs-native-mode"></a>Administrar una base de datos del servidor de informes (Modo nativo de SSRS)
  Una implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa dos bases de datos relacionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenamiento interno. De manera predeterminada, las bases de datos tienen los nombres ReportServer y ReportServerTempdb. ReportServerTempdb se crea con la base de datos principal del servidor de informes y se usa para almacenar datos temporales, información de sesión e informes almacenados en caché.  
  
 En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], entre las tareas de administración de bases de datos se incluyen la copia de seguridad y restauración de bases de datos del servidor de informes y la administración de las claves de cifrado que se usan para cifrar y descifrar datos confidenciales.  
  
 Para administrar las bases de datos del servidor de informes, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona una amplia variedad de herramientas.  
  
-   Para realizar una copia de seguridad, restaurar, mover o recuperar una base de datos del servidor de informes, se puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], los comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] o las utilidades de símbolo del sistema de la base de datos. Para obtener instrucciones, vea [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md) en los Libros en pantalla de SQL Server.  
  
-   Para copiar el contenido de una base de datos existente en otra base de datos del servidor de informes, puede adjuntar una copia de una base de datos del servidor de informes y utilizarla con una instancia distinta del servidor de informes. También puede crear y ejecutar un script que utilice llamadas SOAP para volver a crear contenido del servidor de informes en una nueva base de datos. Puede usar la utilidad **rs** para ejecutar el script.  
  
-   Para administrar las conexiones entre el servidor de informes y la base de datos del servidor de informes, y para averiguar qué base de datos se utiliza para una instancia concreta del servidor de informes, puede utilizarse la página Instalación de base de datos de la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obtener más información sobre la conexión del servidor de informes a la base de datos del servidor de informes, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="sql-server-login-and-database-permissions"></a>Permisos de inicio de sesión y de base de datos de SQL Server  
 Las bases de datos del servidor de informes son utilizadas internamente por este. El servicio del servidor de informes realiza conexiones a cualquier base de datos. Puede usar la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar la conexión del servidor de informes a la base de datos del servidor de informes.  
  
 Las credenciales para la conexión del servidor de informes a la base de datos pueden ser la cuenta de servicio, una cuenta de usuario de dominio o local de Windows o un usuario de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Debe elegir una cuenta existente para la conexión, ya que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no crea cuentas por usted.  
  
 Automáticamente se creará para usted un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la base de datos del servidor de informes para la cuenta especificada.  
  
 Los permisos a la base de datos también se configuran automáticamente. La herramienta de configuración de Reporting Services asignará la cuenta o usuario de la base de datos a los roles `Public` y `RSExecRole` para las bases de datos del servidor de informes. `RSExecRole` otorga permisos para tener acceso a las tablas de base de datos y para ejecutar procedimientos almacenados. El `RSExecRole` se crea en master y msdb al crear la base de datos del servidor de informes. `RSExecRole` es miembro del rol `db_owner` para las bases de datos del servidor de informes, lo que permite al servidor de informes actualizar su propio esquema que admite un proceso de actualización automática.  
  
## <a name="naming-conventions-for-the-report-server-databases"></a>Convenciones de nomenclatura para las bases de datos del servidor de informes  
 Cuando se crea la base de datos principal, su nombre debe seguir las reglas especificadas para los [Identificadores de bases de datos](../../relational-databases/databases/database-identifiers.md). El nombre de la base de datos temporal utiliza siempre el mismo nombre que la base de datos principal del servidor de informes pero con el sufijo Tempdb. No puede elegir un nombre diferente para la base de datos temporal.  
  
 No se permite cambiar el nombre de una base de datos del servidor de informes porque las bases de datos del servidor de informes se consideran componentes internos. Si se cambia el nombre de las bases de datos del servidor de informes, se producen errores. Específicamente, si se cambia el nombre de la base de datos principal, un mensaje de error explica que los nombres de las bases de datos no están sincronizados. Si cambia el nombre de la base de datos ReportServerTempdb, se produce el siguiente error interno más adelante al ejecutar informes:  
  
 "Error interno en el servidor de informes. Vea el registro de errores para obtener más detalles. (rsInternalError)  
  
 El nombre de objeto 'ReportServerTempDB.dbo.PersistedStream' no es válido."  
  
 Este error se debe a que el nombre ReportServerTempdb se almacena internamente y lo utilizan los procedimientos almacenados para realizar operaciones internas. Si se cambia el nombre de la base de datos temporal, no funcionarán correctamente los procedimientos almacenados.  
  
## <a name="enabling-snapshot-isolation-on-the-report-server-database"></a>Habilitar el aislamiento de instantánea en la base de datos del servidor de informes  
 No puede habilitar el aislamiento de instantánea en la base de datos del servidor de informes. Si está activado el aislamiento de instantánea, se producirá el error siguiente: "El informe seleccionado no está preparado para verlo. Aún se está representando o no hay disponible una instantánea de informe".  
  
 Si no habilitó explícitamente el aislamiento de instantánea, puede que el atributo lo estableciera otra aplicación o que la base de datos **modelo** tenga el aislamiento de instantánea habilitado, haciendo que todas las bases de datos nuevas heredaran el valor.  
  
 Para desactivar el aislamiento de instantánea en la base de datos del servidor de informes, inicie Management Studio, abra una nueva ventana de consulta y pegue y después ejecute el script siguiente:  
  
```  
ALTER DATABASE ReportServer  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServerTempdb  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServer  
SET READ_COMMITTED_SNAPSHOT OFF  
ALTER DATABASE ReportServerTempDb  
SET READ_COMMITTED_SNAPSHOT OFF  
```  
  
## <a name="about-database-versions"></a>Acerca de las versiones de base de datos  
 En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]no se dispone de información explícita acerca de la versión de la base de datos. Sin embargo, como las versiones de la base de datos siempre están sincronizadas con las versiones de los productos, se puede utilizar la información de la versión del producto para saber cuándo ha cambiado la versión de la base de datos. Información de versión del producto de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se indica a través de la información de versión del archivo que aparece en los archivos de registro en los encabezados de todas las llamadas SOAP, y cuando se conecta a la URL del servidor de informes (por ejemplo, cuando abre un explorador para http://localhost/reportserver).  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Crear una base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Operaciones de copia de seguridad y restauración de Reporting Services](../install-windows/backup-and-restore-operations-for-reporting-services.md)   
 [Base de datos del servidor de informes &#40;Modo nativo de SSRS&#41;](report-server-database-ssrs-native-mode.md)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](reporting-services-report-server-native-mode.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
