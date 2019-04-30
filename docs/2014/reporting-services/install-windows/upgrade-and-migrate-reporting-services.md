---
title: Actualizar y migrar Reporting Services | Microsoft Docs
ms.prod: sql-server-2014
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 2ef6c53e1cb9fd11eb8cba6bb788de9b9b1fe10a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63144591"
---
# <a name="upgrade-and-migrate-reporting-services"></a>Upgrade and Migrate Reporting Services

Este tema ofrece información general de las opciones de actualización y migración para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Hay dos enfoques generales para actualizar una implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   **Actualización:** Actualizar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componentes en los servidores y las instancias donde están instalados actualmente. Habitualmente se denomina actualización "en contexto". No se admite la actualización en contexto de un modo de servidor de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a otro. Por ejemplo, no puede actualizar un servidor de informes en modo nativo a un servidor de informes en modo de SharePoint. Puede migrar los elementos de informe de un modo a otro. Para obtener más información, consulte la sección 'Nativo para la migración de SharePoint' más adelante en este documento y el tema relacionado [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
-   **Migrar**: Instalar y configurar un nuevo entorno de SharePoint, copiar los elementos de informe y los recursos en el nuevo entorno y configura el nuevo entorno para usar contenido existente. Una forma de nivel inferior de migración es copiar bases de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , los archivos de configuración y, si se usa el modo de SharePoint, las bases de datos de contenido de SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
  
##  <a name="bkmk_top"></a> En este tema:  
  
-   [Problemas conocidos de actualización y los procedimientos recomendados](#bkmk_known_issues)  
  
-   [Instalaciones en paralelo](#bkmk_side_by_side)  
  
-   [Actualización en contexto](#bkmk_inplace_upgrade)  
  
-   [Lista de comprobación previa a la actualización](#bkmk_upgrade_checklist)  
  
-   [Escenarios de migración y actualización del modo nativo](#bkmk_native_scenarios)  
  
-   [Actualizar una implementación de escalabilidad horizontal de modo nativo de Reporting Services](#bkmk_native_scaleout)  
  
-   [Escenarios de migración y actualización del modo de SharePoint](#bkmk_sharePoint_scenarios)  
  
-   [Consideraciones para una migración](#bkmk_migration_considerations)  
  
-   [Recursos adicionales](#bkmk_additional_resources)  
  
##  <a name="bkmk_known_issues"></a> Problemas conocidos y prácticas recomendadas de actualización  
 Para obtener una lista detallada de las ediciones y las versiones admitidas que puede actualizar, vea [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
> [!TIP]
>  Para obtener la información más reciente sobre los problemas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vea lo siguiente:  
> 
>  -   [Notas de la versión de SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
> -   [Sugerencias, trucos y solución de problemas de SQL Server 2014 Reporting Services](https://go.microsoft.com/fwlink/?LinkID=391254).  
> -   Use el Asesor de actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [problemas de actualización de Reporting Services &#40;Upgrade Advisor&#41; ](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md) y [Cómo: Instalar el Asesor de actualizaciones](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md).  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
##  <a name="bkmk_side_by_side"></a> Instalaciones en paralelo  
 El modo nativo de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] se puede instalar en paralelo con una implementación de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] en modo nativo.  
  
 No se admiten las implementaciones en paralelo del modo de SharePoint de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] y ninguna de las versiones anteriores de los componentes del modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
##  <a name="bkmk_inplace_upgrade"></a> Actualización en contexto  
 El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ocupa de realizar la actualización. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede usar para actualizar algunos o todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluido [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. El programa de instalación detecta las instancias existentes y solicita que se actualice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El programa de instalación proporciona opciones de actualización que puede especificar como argumentos de la línea de comandos o en el Asistente para la instalación.  
  
 Al ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede seleccionar la opción para actualizar desde una de las versiones siguientes o puede instalar una nueva instancia de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] que se ejecute en paralelo con las instalaciones existentes:  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 Para obtener más información sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea lo siguiente  
  
||  
|-|  
|[Actualizar a SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)|  
|[Actualización a SQL Server 2014 mediante el Asistente para instalación &#40;el programa de instalación&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|  
|[Instalar SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)|  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
##  <a name="bkmk_upgrade_checklist"></a> Lista de comprobación previa a la actualización  
 Antes de actualizarse a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], revise lo siguiente:  
  
-   Revise los requisitos para determinar si el hardware y el software pueden admitir [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]. Para obtener más información, vea [Hardware and Software Requirements for Installing SQL Server 2014](../../../2014/sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Utilice el Comprobador de configuración del sistema (SCC) para examinar el equipo del servidor de informes en busca de cualquier condición que pudiera evitar la instalación correcta de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md).  
  
-   Revise las prácticas recomendadas de seguridad y orientación para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Security Considerations for a SQL Server Installation](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
-   Ejecute el Asesor de actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo del servidor de informes para determinar cualquier problema que pueda impedir que la actualización se realice correctamente. Para obtener más información, vea [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
-   Haga una copia de seguridad de la clave simétrica. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
-   Haga copia de seguridad de las bases de datos del servidor de informes y de los archivos de configuración. Para obtener más información, vea [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md).  
  
-   Haga copia de seguridad de las personalizaciones de los directorios virtuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] existentes en IIS.  
  
-   Quite los certificados SSL no válidos.  Se trata de los certificados expirados y que no piensa actualizar antes de actualizar Reporting Services.  Los certificados no válidos provocará un error de actualización y se escribirá un mensaje de error similar al siguiente en el archivo de registro de Reporting Services: **Microsoft.ReportingServices.WmiProvider.WMIProviderException: Un certificado de capa de Sockets seguros (SSL) no está configurado en el sitio Web.** .  
  
 Antes de actualizar un entorno de producción, ejecute siempre una actualización de prueba en un entorno de preproducción que tenga la misma configuración que el entorno de producción.  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
## <a name="overview-of-migration-scenarios"></a>Información general de los escenarios de migración  
 Si va a realizar una actualización desde una versión admitida de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], normalmente puede ejecutar el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el fin de actualizar los archivos de programa, la base de datos y todos los datos de aplicación del servidor de informes.  
  
 Sin embargo, es necesario **migrar** manualmente la instalación de un servidor de informes si se da alguna de las condiciones siguientes:  
  
-   El Asesor de actualizaciones ha detectado uno o varios bloqueos de la actualización. Para obtener más información, vea [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
-   Desea cambiar el tipo de servidor de informes usado en la implementación. Por ejemplo, no puede actualizar o convertir un servidor de informes en modo nativo al modo de SharePoint. Para obtener más información, vea [Migración del modo nativo al modo de SharePoint &#40;SSRS&#41;](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md).  
  
-   Desea minimizar la cantidad de tiempo que el servidor de informes está sin conexión durante el proceso de actualización. La instalación actual permanece en línea mientras copia datos de contenido en una instancia del servidor de informes y prueba la instalación sin cambiar el estado de la instalación del servidor de informes existente.  
  
-   Es recomendable migrar una implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de SharePoint 2010 a SharePoint 2013. SharePoint 2013 no admite la actualización en contexto desde SharePoint 2010. Para obtener más información, vea [Migrar una instalación de Reporting Services &#40;modo de SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
##  <a name="bkmk_native_scenarios"></a> Escenarios de actualización y migración en modo nativo  
 **Actualización:** Actualización en contexto para el modo nativo es el mismo proceso para cada una de las versiones admitidas enumeradas anteriormente en este tema. Ejecute el Asistente para la instalación de SQL Server o una instalación desde la línea de comandos. Después de la instalación, la base de datos del servidor de informes se actualizará automáticamente al nuevo esquema de la base de datos del servidor de informes. Para obtener más información, vea la sección [In-place upgrade](#bkmk_inplace_upgrade) en este tema.  
  
 El proceso de actualización comienza al seleccionar una instancia del servidor de informes existente para actualizar.  
  
1.  Si la base de datos del servidor de informes está en un equipo remoto y no dispone del permiso para actualizarla, el programa de instalación le solicita que proporcione las credenciales para actualizar a una base de datos del servidor de informes remota. Asegúrese de proporcionar las credenciales que tiene `sysadmin` o los permisos de actualización de base de datos.  
  
2.  El programa de instalación comprueba la configuración o las condiciones que impiden la actualización y lee los valores de configuración. Algunos ejemplos pueden ser las extensiones personalizadas que se implementan en el servidor de informes. Si la actualización permanece bloqueada, debe modificar la instalación para que deje de estarlo o migrar a una nueva instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obtener más información, vea la documentación del Asesor de actualizaciones.  
  
3.  Si la actualización puede continuar, el programa de instalación le solicita que continúe con el proceso de actualización.  
  
4.  El programa de instalación crea carpetas nuevas para los archivos de programa de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Las carpetas de programas para una [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalación incluyen MSRS12.\< *nombre de instancia*>.  
  
5.  El programa de instalación agrega los archivos de programa del servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , las herramientas de configuración y las utilidades de línea de comandos que forman parte de la característica del servidor de informes.  
  
    1.  Los archivos de programa de la versión anterior se quitan.  
  
    2.  Entre las has herramientas de configuración del servidor de informes y las utilidades que se actualizan a la nueva versión se incluyen la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo, utilidades de la línea de comandos como RS.exe y el Generador de informes.  
  
    3.  Otras herramientas cliente como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y los Libros en pantalla no se actualizan. Para obtener nuevas versiones de las herramientas, puede agregarlas al ejecutar la instalación. Las versiones anteriores coexistirán con las versiones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Si instaló ejemplos, la versión anterior permanecerá. El programa de instalación no admite la actualización de los ejemplos de SQL Server.  
  
    4.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] es una descarga independiente. Para obtener más información, vea [Microsoft SQL Server 2014 Data Tools - Business Intelligence para Microsoft Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843).  
  
6.  El programa de instalación reutiliza la entrada de servicio del Administrador de control de servicios para el servicio Servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Esta entrada de servicio incluye la cuenta de servicio de Windows Servidor de informes.  
  
7.  El programa de instalación reserva direcciones URL nuevas de acuerdo con la configuración actual del directorio de IIS. Es posible que el programa de instalación no quite los directorios virtuales en IIS, de modo que tiene que asegurarse de quitarlos manualmente una vez finalizada la actualización.  
  
8.  El programa de instalación actualiza las bases de datos del servidor de informes al nuevo esquema y modifica `RSExecRole` agregando permisos de propietario de base de datos al rol. Este paso solamente se produce cuando se está actualizando desde la versión [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anterior a SP1.  
  
9. El programa de instalación combina los valores de los archivos de configuración. Utilizando como base los archivos de configuración de instalación de la instalación actual, se agregan las nuevas entradas. No se quitan las entradas desusadas, pero el servidor de informes dejará de leerlas una vez finalizada la actualización. La actualización no eliminará los archivos de registro anteriores, el archivo RSWebApplication.config obsoleto o la configuración de directorios virtuales en IIS. La actualización no quitará el Diseñador de informes de SQL Server 2005, Management Studio u otras herramientas de cliente. Si ya no los necesita, asegúrese de quitar estos archivos y herramientas una vez finalizada la actualización.  
  
 **Migración:** Migración de una versión anterior de una instalación en modo nativo a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] consta de los mismos pasos para todas las versiones admitidas que aparecen anteriormente en este tema. Para obtener más información, vea [Migrar una instalación de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
##  <a name="bkmk_native_scaleout"></a> Actualizar una implementación escalada horizontalmente de Reporting Services en modo nativo  
 A continuación se muestra un resumen de cómo actualizar una implementación en modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] escalada horizontalmente a más de un servidor de informes. Este proceso requiere un tiempo de inactividad de la implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
1.  Haga copia de seguridad de las claves de cifrado y las bases de datos del servidor de informes. Para obtener más información, vea [Operaciones de copia de seguridad y restauración de Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md) y [Agregar y quitar claves de cifrado para implementaciones escaladas &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).  
  
2.  Use el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y quite todos los servidores de informes de la implementación escalada. Para obtener más información, vea [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
3.  Actualice uno de los servidores de informes a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
4.  Use el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para volver a agregar los servidores de informes a la implementación escalada. Para obtener más información, vea [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
     Para cada servidor, repita los pasos de actualización y escalado horizontal.  
  
##  <a name="bkmk_sharePoint_scenarios"></a> Escenarios de actualización y migración en modo de SharePoint  
 En las próximas secciones se describen los problemas y los pasos básicos necesarios para actualizar o migrar desde versiones especificadas en modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] al modo de SharePoint de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Hay dos componentes de instalación para actualizar una implementación del modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    > [!TIP]  
    >  Use el cmdlet [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de SharePoint de `Get-SPRSServiceApplicationServers` para determinar los servidores de la granja de servidores de SharePoint que están ejecutando actualmente el servicio compartido de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y, por tanto, requieren una actualización.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Complemento para productos de SharePoint. Para obtener más información, consulte [instalar o desinstalar el complemento Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
 Para obtener los pasos detallados sobre cómo migrar una instalación en modo de SharePoint, vea [Migrar una instalación de Reporting Services &#40;modo de SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
> [!IMPORTANT]  
>  Algunos de los escenarios siguientes necesitan un tiempo de inactividad del entorno de SharePoint debido a las diversas tecnologías que hay que actualizar. Si su situación no permite que haya tiempo de inactividad, necesitará completar una migración en lugar de una actualización en contexto.  
  
### <a name="includesssql11includessssql11-mdmd-to-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 **Entorno inicial:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]y SharePoint 2010.  
  
 **Entorno final:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SQL Server 2010 o SharePoint 2013.  
  
-   **SharePoint 2010:** Actualización de local [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es compatible, pero el escenario de actualización requiere un tiempo de inactividad del entorno de SharePoint.  
  
     Si también desea que el entorno final ejecute SharePoint 2013, debe completar una operación de actualizar y adjuntar la base de datos de SharePoint 2010 a SharePoint 2013.  
  
-   **SharePoint 2013:** SharePoint 2013 no admite la actualización en contexto desde SharePoint 2010. Pero se admite el procedimiento de **actualizar y adjuntar la base de datos**  . El comportamiento es diferente de la actualización a SharePoint 2010, donde un cliente puede elegir entre los dos métodos básicos de actualización: actualización en contexto y actualizar y adjuntar la base de datos.  
  
     Si tiene una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada con SharePoint 2010, no puede realizar una actualización en contexto del servidor de SharePoint. Sin embargo, puede migrar las bases de datos de contenido y las bases de datos de aplicación de servicio de la granja de SharePoint 2010 a una granja de SharePoint 2013.  
  
### <a name="includesskilimanjaroincludessskilimanjaro-mdmd-to-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 **Entorno inicial:** SQL Server 2008 R2, SharePoint 2010.  
  
 **Entorno final:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]y SharePoint 2010.  
  
-   Se admite la actualización en contexto y no hay ningún tiempo de inactividad para el entorno de SharePoint.  
  
-   Instale la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint en cada servidor web front-end de la granja. Puede instalar el complemento mediante el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o descargándolo.  
  
-   Ejecute [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalación para actualizar el modo de SharePoint para cada servidor de informes' '. El Asistente para instalación de SQL Server instalará el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Service y cree una nueva aplicación de servicio.  
  
     Si también desea que el entorno final ejecute SharePoint 2013, debe completar una operación de actualizar y adjuntar la base de datos de SharePoint 2010 a SharePoint 2013.  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
### <a name="includesskatmaiincludessskatmai-mdmd-sp2-to-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2 a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 **Entorno inicial:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2, SharePoint 2007.  
  
 **Entorno final:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]y SharePoint 2010.  
  
-   Este escenario de actualización en contexto necesita un tiempo de inactividad del entorno de SharePoint porque hay que actualizar las tecnologías de SharePoint y SQL Server. Puede que le interese completar una migración en lugar de una actualización en contexto.  
  
-   Actualice [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] al Service Pack 2 (SP2) primero, si no lo ha hecho ya.  
  
-   Actualice SharePoint a 2010. Cuando ejecute el instalador de requisitos previos de SharePoint 2010, actualizará el complemento Reporting Services para Productos de SharePoint 2010.  
  
-   Instale la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint en todos los front-end web de SharePoint. El instalador de requisitos previos de SharePoint instaló la versión SQL Server 2008 R2 del complemento pero se necesita la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para trabajar con un servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
-   > [!WARNING]  
    >  Después de la actualización de SharePoint, el entorno de Reporting Services no funcionará hasta que no se actualice SQL Server.  
  
-   Actualice [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Al ejecutar el Asistente para la instalación de SQL server, aparecerá un cuadro de diálogo**Autenticación del modo de SharePoint de SQL Server Reporting Services**. Se instalará el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y las credenciales de la página de autenticación se usarán para crear un nuevo grupo de aplicaciones de SharePoint.  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
### <a name="sql-server-2005-sp2-to-includesssql14includessssql14-mdmd"></a>SQL Server 2005 SP2 a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 **Entorno inicial:** SQL Server 2005 SP2, SharePoint 2007.  
  
 **Entorno final:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]y SharePoint 2010.  
  
-   Este escenario de actualización en contexto necesita un tiempo de inactividad del entorno de SharePoint porque hay que actualizar las tecnologías de SharePoint y SQL Server. Puede que le interese completar una migración en lugar de una actualización en contexto.  
  
-   Actualice SQL Server 2005 al Service Pack 2 (SP2) primero, si no lo ha hecho ya.  
  
-   Actualice SharePoint a SharePoint 2010. Cuando ejecute el instalador de requisitos previos de SharePoint 2010, actualizará el complemento Reporting Services para Productos de SharePoint 2010.  
  
-   > [!WARNING]  
    >  Después de la actualización de SharePoint, el entorno de Reporting Services no funcionará hasta que no se actualice SQL Server.  
  
-   Instale la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint en todos los front-end web de SharePoint. El instalador de requisitos previos de SharePoint instaló la versión SQL Server 2008 R2 del complemento pero se necesita la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para trabajar con un servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
-   Actualice [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Al ejecutar el Asistente para la instalación de SQL server, aparecerá un cuadro de diálogo "Autenticación del modo de SharePoint de SQL Server Reporting Services". Se instalará el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y las credenciales de la página de autenticación se usarán para crear un nuevo grupo de aplicaciones de SharePoint.  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
##  <a name="bkmk_migration_considerations"></a> Consideraciones sobre una migración  
 Al mover los datos de la aplicación, debe ser consciente de los aspectos y restricciones siguientes:  
  
-   La protección de la clave de cifrado incluye un hash que incorpora la identidad del equipo.  
  
-   Los nombres de base de datos del servidor de informes son fijos y no se pueden cambiar en el equipo nuevo.  
  
### <a name="encryption-key-considerations"></a>Consideraciones sobre las claves de cifrado  
 Realice siempre una copia de seguridad de las claves de cifrado antes de mover una base de datos del servidor de informes a otro equipo.  
  
 Al mover una instalación del servidor de informes a otro equipo, invalidará el hash que protege las claves de cifrado que se usan para proteger los datos confidenciales almacenados en la base de datos del servidor de informes. Cada instancia del servidor de informes que utiliza la base de datos tiene su copia de la clave de cifrado, que se cifra con la identidad de la cuenta de servicio que está definida en el equipo actual. Si cambia los equipos, el servicio dejará de tener acceso a la clave, aunque utilice el mismo nombre de cuenta en el equipo nuevo.  
  
 Para volver a establecer el cifrado reversible en el nuevo equipo del servidor de informes, debe restaurar la clave de la que realizó anteriormente una copia de seguridad. El conjunto de claves completo que se almacena en la base de datos del servidor de informes está compuesto de un valor de clave simétrica más la información de identidad del servicio que se usa para restringir el acceso a la clave, para que solo pueda usarla la instancia del servidor de informes donde se almacenó. Durante la restauración de la clave, el servidor de informes reemplaza las copias existentes de la clave por las versiones nuevas. La versión nueva incluye los valores de identidad de servicio y de equipo definidos en el equipo actual. Para obtener más información, vea los temas siguientes:  
  
-   Modo SharePoint: Consulte la sección "Administración de claves" de [administrar una aplicación de servicio de SharePoint de Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
-   Modo nativo: Consulte [copia de seguridad y restaurar claves de cifrado Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
### <a name="fixed-database-name"></a>Nombre fijo de la base de datos  
 No se puede cambiar el nombre de la base de datos del servidor de informes. La identidad de la base de datos se registra en los procedimientos almacenados del servidor de informes cuando se crea la base de datos. El cambio del nombre de las bases de datos temporales o principales del servidor de informes hará que se produzcan errores cuando se ejecuten los procedimientos, lo que invalida la instalación del servidor de informes.  
  
 Si el nombre de la base de datos de la instalación existente no es adecuado para la instalación nueva, plantéese la posibilidad de crear una base de datos nueva con el nombre que prefiera y, a continuación, cargar los datos de la aplicación existente mediante las técnicas siguientes:  
  
-   Escriba un script de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que llame a los métodos SOAP del servicio web del servidor de informes para copiar datos entre las bases de datos. Para ejecutar el script, puede usar la utilidad RS.exe. Para obtener más información sobre este método, vea [Scripting and PowerShell with Reporting Services (Scripting y PowerShell con Reporting Services)](../tools/scripting-and-powershell-with-reporting-services.md).  
  
-   Escriba código que llame al proveedor de WMI para copiar datos entre las bases de datos. Para obtener más información sobre este método, vea [Access the Reporting Services WMI Provider (Obtener acceso al proveedor de WMI de Reporting Services)](../tools/access-the-reporting-services-wmi-provider.md).  
  
-   Si solo tiene unos pocos elementos, puede volver a publicar los informes, los modelos de informe y los orígenes de datos compartidos del Diseñador de informes, del Diseñador de modelos y del Generador de informes en el nuevo servidor de informes. Debe volver a crear asignaciones de roles, suscripciones, programaciones compartidas, calendarios de instantáneas de informes, propiedades personalizadas que establezca en informes u otros elementos, seguridad de elementos de modelo y propiedades que establezca en el servidor de informes. Perderá el historial de informes y los datos del registro de ejecución de informes.  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
##  <a name="bkmk_additional_resources"></a> Recursos adicionales  
  
> [!NOTE]  
>  Para obtener más información acerca de cómo actualizar y adjuntar la base de datos de SharePoint 2013, vea lo siguiente:  
  
-   [Información general del proceso de actualización a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688) (https://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Limpiar un entorno antes de una actualización a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689) (https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Actualizar las bases de datos de SharePoint 2010 a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
 ![Icono de flecha usado con el vínculo volver al principio](../../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema:](#bkmk_top)  
  
## <a name="see-also"></a>Vea también  
 [Actualizar informes](../../reporting-services/install-windows/upgrade-reports.md)   
 [Actualización a SQL Server 2014 mediante el Asistente para instalación &#40;el programa de instalación&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
