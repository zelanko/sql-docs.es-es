---
title: Conectarse a un servidor de informes de modo nativo | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 703e25f513fa8482d62d8c454aca1dbe0edea92a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112399"
---
# <a name="connect-to-a-native-mode-report-server"></a>Conectarse a un servidor de informes en modo nativo
  Utilice este cuadro de diálogo para conectarse a un local o remota [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o una versión posterior [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instancia del servidor de informes. No se puede usar esta herramienta para conectarse a versiones anteriores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidores de informes. Solo puede conectarse a una instancia cada vez.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  El [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager no se usa para configurar y administrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] el modo de SharePoint. Puede usar scripts de Administración central de SharePoint y de PowerShell para configurar un servidor de informes en modo de SharePoint. Para obtener más información, vea [instalar Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
> [!TIP]  
>  El[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (RSConfigTool.exe) se instala con un nivel de privilegios "highestAvailable". Este comportamiento es así por diseño. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] precisa la comunicación con las API WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Una parte de la comunicación WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requiere un nivel superior o administrativo de privilegios.  
  
-   Para conectarse a una instancia local del servidor de informes, utilice los valores predeterminados y haga clic en **Conectar**. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona el nombre del servidor local y detecta la instancia predeterminada. En la mayoría de los casos, puede hacer clic en **Conectar** sin que tenga que cambiar los valores. Si instaló más de una instancia, debe seleccionar la que desea utilizar.  
  
-   Para conectarse a una instancia remota del servidor de informes, escriba el nombre del servidor, haga clic en **Buscar**, seleccione la instancia y, a continuación, haga clic en **Conectar**.  
  
 Para abrir este cuadro de diálogo, inicie la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Este cuadro de diálogo aparece inmediatamente al iniciar la herramienta. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de servidor**  
 Escriba el nombre de red del equipo en el que [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o una versión posterior [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está instalado. Basta con que escriba el nombre de equipo; no incluya ningún prefijo ni barras diagonales.  
  
 **Buscar**  
 Busque el equipo especificado en **Nombre del servidor**.  
  
 **Instancia del servidor de informes**  
 Seleccione la instancia a la que conectarse si se instalan varias instancias del servidor de informes. Solo las instancias válidas están disponibles para la selección. Si está ejecutando versiones anteriores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] side-by-side un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia, esas instancias no aparecerán en la lista.  
  
 **Conectar**  
 Conéctese al servidor y cree las instancias que especifique.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  