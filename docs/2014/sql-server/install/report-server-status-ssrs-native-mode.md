---
title: Estado del servidor de informes (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serverstatus.F1
ms.assetid: 2f63ad1c-1bc2-449d-b451-fb39a0060838
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 15a177080792eb26273399f41aad577962885376
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952457"
---
# <a name="report-server-status-ssrs-native-mode"></a>Estado del servidor de informes (Modo nativo de SSRS)
  Utilice esta página para ver información sobre la instancia del servidor de informes a la que está conectado actualmente. Esta página es la página de inicio para la configuración del servidor de informes. Hay páginas adicionales disponibles para configurar las direcciones URL, la cuenta de servicio, la base de datos del servidor de informes, la distribución del correo electrónico del servidor de informes, una implementación que permita una ampliación con varios servidores y las claves de cifrado.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para abrir esta página, inicie el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la instancia del servidor de informes. Para obtener más información, [vea &#40;administrador de configuración de Reporting Services&#41;del](reporting-services-configuration-manager-native-mode.md).  
  
> [!TIP]  
>  El Configuration Manager @ no__t-0 (RSConfigTool. exe) se instala con un nivel de privilegios "highestAvailable". Este comportamiento es así por diseño. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] precisa la comunicación con las API WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una parte de la comunicación WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requiere un nivel superior o administrativo de privilegios.  
  
 Si se conecta al servidor de informes y todos los vínculos de página están deshabilitados, compruebe que se ha iniciado el servicio del servidor de informes. **Estado del servicio de informes:** Debe ser "Started". También puede usar la aplicación de consola Servicios en Herramientas administrativas para comprobar el estado del servicio.  
  
## <a name="options"></a>Opciones  
 **Instancia de SQL Server**  
 Muestra información sobre la instancia del servidor de informes a la que está conectado actualmente. Los nombres de instancia del servidor de informes se basan en las instancias con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La instancia predeterminada es MSSQLSERVER. Una instancia con nombre será un valor que especifique durante la instalación. Para obtener más información acerca de las instancias, vea [trabajar con varias versiones e instancias de SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md) en los libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  En SQL Server Express con Advanced Services, la instancia predeterminada es SQLEXPRESS.  
  
 **Id. de instancia**  
 Corresponde a una carpeta en el sistema de archivos que almacena los archivos de programa para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que está conectado. El valor de **Id. de instancia** lo asigna el programa de instalación en el formato *componente*.*instancia*, donde *componente* es un valor que significa un componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e *instancia* es un nombre de instancia. El nombre de instancia predeterminado es MSSQLSERVER. Por ejemplo, si instala instancias predeterminadas de los componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , los nombres de carpeta correspondientes son los siguientes:  
  
-   MSSQL12.MSSQLSERVER  
  
-   MSAS12.MSSQLSERVER  
  
-   MSRS12.MSSQLSERVER  
  
 Si instala una segunda instancia de un componente que ya instaló, como el [!INCLUDE[ssDE](../../includes/ssde-md.md)], y asigna el nombre Contoso a la instancia, el **Id. de instancia** es MSSQL12.Contoso.  
  
 **Edición**  
 Muestra información de la edición. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server](https://go.microsoft.com/fwlink/?linkid=232473).  
  
 **Versión del producto**  
 Muestra la versión de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que instaló.  
  
 **Base de datos del servidor de informes**  
 Muestra el nombre de la base de datos del servidor de informes que almacena los datos de la aplicación para la instancia del servidor de informes actual.  
  
 **Modo de servidor de informes**  
 Debe mostrar siempre el valor **Nativo**. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] solo admite servidores de informes en modo nativo. Si se muestra el valor **Modo integrado de SharePoint**, puede indicar que la implementación de modo nativo no está configurada correctamente y es necesario conectarse a un catálogo de informes de modo nativo. Use la página **Base de datos** del administrador de configuración para cambiar la base de datos y crear una nueva base de datos o para conectarse a un catálogo existente de bases de datos del servidor de informes de modo nativo.  
  
 **Estado del servidor**  
 Muestra si el servicio Servidor de informes está ejecutándose.  
  
 **Iniciar**  
 Inicia el servicio Servidor de informes. Es necesario reiniciar el servicio tras algunos cambios de configuración (por ejemplo, al reconfigurar el servidor de informes después de un cambio de nombre de equipo). Si reconfigura las reservas de direcciones URL, el servicio se reiniciará automáticamente. Es necesario reiniciar para que los cambios se reconozcan.  
  
 **Detener**  
 Detiene el servicio Servidor de informes. Al detener el servicio, se detiene el funcionamiento del servidor de informes. Para obtener más información, vea [iniciar y detener el servicio del servidor de informes en los](../../reporting-services/report-server/start-and-stop-the-report-server-service.md) libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services temas &#40;de ayuda de F1 en&#41;el modo nativo de SSRS](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Administrador de configuración de Reporting Services &#40;del&#41;](/sql/sql-server/install/reporting-services-configuration-manager-native-mode)   
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
