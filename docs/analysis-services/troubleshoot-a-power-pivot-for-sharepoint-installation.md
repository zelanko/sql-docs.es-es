---
title: "Solucionar problemas de una instalaci&#243;n de PowerPivot para SharePoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Solucionar problemas de una instalaci&#243;n de PowerPivot para SharePoint
  Si obtiene errores en lugar de las páginas y características que espera, haga lo siguiente.  
  
-   Revise las notas de la versión para SharePoint y [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] con el fin de conocer soluciones alternativas para los problemas de instalación conocidos. Las notas de la versión se proporcionan con los discos de instalación o en el sitio de Microsoft del que descargó el software.  
  
    -   [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)  
  
-   Vea el tema de wiki de TechNet [Troubleshooting Installations of Power Pivot (and other add-ins)](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx) (Solucionar problemas de instalaciones de PowerPivot [y otros complementos]).  
  
## Problemas  
  
### Las imágenes en miniatura de la galería de PowerPivot se muestran como una X roja  
 Una causa posible es que **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para colecciones de sitios** no esté activa. Haga lo siguiente:  
  
1.  En la biblioteca de la galería de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], haga clic en **Configuración del sitio** desde el icono de engranaje ![Configuración de SharePoint](../analysis-services/media/as-sharepoint2013-settings-gear.png "Configuración de SharePoint") o la lista **Inicio**.  
  
2.  En la sección **Administración de la colección de sitios** , haga clic en **Características de la colección de sitios**.  
  
3.  Haga clic en **Características de la colección de sitios**.  
  
4.  Compruebe que **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para colecciones de sitios** tiene el valor **Activa**.  
  
 Para conocer otras causas de este problema, vea [Power Pivot Gallery shows Red X's for Icons](http://support.microsoft.com/kb/2361559) (La galería de PowerPivot muestra letras X rojas para los iconos), en http://support.microsoft.com/kb/2361559.  
  
  