---
title: Conectarse a un servidor de informes en modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5bf32c8427679b342bee89d6541b051beed2e8ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952287"
---
# <a name="connect-to-a-native-mode-report-server"></a>Conectarse a un servidor de informes en modo nativo
  Utilice este cuadro de diálogo para conectarse a una instancia del servidor de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o posterior, local o remota. No puede usar esta herramienta para conectarse a las versiones anteriores de los servidores de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Solo puede conectarse a una instancia cada vez.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo.  
  
> [!NOTE]  
>  El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se usa para configurar y administrar el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Puede usar scripts de Administración central de SharePoint y de PowerShell para configurar un servidor de informes en modo de SharePoint. Para más información, consulte [Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
> [!TIP]  
>  El[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager (RSConfigTool. exe) se instala con un nivel de privilegios "highestAvailable". Este comportamiento es así por diseño. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] precisa la comunicación con las API WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una parte de la comunicación WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requiere un nivel superior o administrativo de privilegios.  
  
-   Para conectarse a una instancia local del servidor de informes, utilice los valores predeterminados y haga clic en **Conectar**. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona el nombre del servidor local y detecta la instancia predeterminada. En la mayoría de los casos, puede hacer clic en **Conectar** sin que tenga que cambiar los valores. Si instaló más de una instancia, debe seleccionar la que desea utilizar.  
  
-   Para conectarse a una instancia remota del servidor de informes, escriba el nombre del servidor, haga clic en **Buscar**, seleccione la instancia y, a continuación, haga clic en **Conectar**.  
  
 Para abrir este cuadro de diálogo, inicie el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Este cuadro de diálogo aparece inmediatamente al iniciar la herramienta. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Nombre del servidor**  
 Escriba el nombre de red del equipo en el que está instalado [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o posterior. Basta con que escriba el nombre de equipo; no incluya ningún prefijo ni barras diagonales.  
  
 **Localización**  
 Busque el equipo especificado en **Nombre del servidor**.  
  
 **Instancia del servidor de informes**  
 Seleccione la instancia a la que conectarse si se instalan varias instancias del servidor de informes. Solo las instancias válidas están disponibles para la selección. Si ejecuta versiones anteriores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en paralelo con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , esas instancias no aparecerán en la lista.  
  
 **Conectar**  
 Conéctese al servidor y cree las instancias que especifique.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
