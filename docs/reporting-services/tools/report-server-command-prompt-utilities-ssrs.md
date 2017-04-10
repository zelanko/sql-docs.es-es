---
title: "Utilidades del s&#237;mbolo del sistema del servidor de informes (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "rsconfig, utilidad"
  - "componentes [Reporting Services], utilidades de línea de comandos"
  - "rs, utilidad"
  - "utilidades del símbolo del sistema [Reporting Services]"
  - "rskeymgmt (utilidad)"
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
caps.latest.revision: 48
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 48
---
# Utilidades del s&#237;mbolo del sistema del servidor de informes (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye varias utilidades de la línea de comandos que se pueden utilizar para administrar un servidor de informes. Estas utilidades se instalan automáticamente cuando se instala el servidor de informes.  
  
|Nombre|Archivo de comandos|Modo de implementación admitido|Description|  
|----------|------------------|-------------------------------|-----------------|  
|Utilidad RSS|rs.exe|Modo nativo y modo de SharePoint. La compatibilidad con el modo de SharePoint se introdujo con la versión [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .|La [utilidad rs](../../reporting-services/tools/rs-exe-utility-ssrs.md) es un host de script que se puede utilizar para llevar a cabo operaciones de script. Use esta herramienta para ejecutar scripts de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que copian datos entre distintas bases de datos del servidor de informes, publican informes, crean elementos en una base de datos del servidor de informes, etc. Para más información sobre cómo usar scripts para administrar un servidor, vea [Script para tareas administrativas y de implementación](../../reporting-services/tools/script-deployment-and-administrative-tasks.md).|  
|Cmdlets de Powershell||Solo SharePoint|Para consultar una lista de los cmdlets de PowerShell, vea [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).|  
|Utilidad Rsconfig|rsconfig.exe|Solo nativo|La utilidad [rsconfig](../../reporting-services/tools/rsconfig-utility-ssrs.md) se utiliza para configurar y administrar una conexión del servidor de informes con la base de datos del servidor de informes. También puede utilizarla para especificar la cuenta de usuario que se va a utilizar para el procesamiento de informes desatendidos. Para más información, vea [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md). Para más información sobre la configuración de la conexión, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|  
|Utilidad Rskeymgmt|rskeymgmt.exe|Solo nativo|La utilidad [rskeymgmt](../../reporting-services/tools/rskeymgmt-utility-ssrs.md) es una herramienta de administración de claves de cifrado. Puede utilizarla para realizar copias de seguridad, aplicar y volver a crear claves simétricas. También puede utilizar esta herramienta para adjuntar una instancia del servidor de informes a una base de datos compartida del servidor de informes. Rskeymgmt puede utilizarse en operaciones de recuperación de base de datos. Para volver a utilizar una base de datos existente en una nueva instalación, aplique una copia de seguridad de la clave simétrica. Si las claves no se pueden recuperar, esta herramienta proporciona un método para eliminar el contenido cifrado que ya no utilice. Para más información sobre la administración de claves y el almacenamiento de información confidencial, vea [Almacenar datos cifrados del servidor de informes &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/store-encrypted-report-server-data-ssrs-configuration-manager.md) y [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-and-manage-encryption-keys-ssrs-configuration-manager.md).|  
  
> [!NOTE]  
>  Si prefiere usar una herramienta que tenga una interfaz gráfica de usuario, puede usar el Administrador de configuración de Reporting Services en lugar de **rsconfig** y **rskeymgmt**.  
  
## Vea también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Herramientas de Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)  
  
  