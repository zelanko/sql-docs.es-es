---
title: Solucionar problemas de un PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a80e3134fc734f962fa9b082374dc3f9c4a74ba2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147255"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Solucionar problemas de una instalación de PowerPivot para SharePoint
  Si obtiene errores en lugar de las páginas y características que espera, haga lo siguiente.  
  
-   Revise las notas de la versión para SharePoint y [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con el fin de conocer soluciones alternativas para los problemas de instalación conocidos. Las notas de la versión se proporcionan con los discos de instalación o en el sitio de Microsoft del que descargó el software.  
  
    -   [Notas de la versión de SQL Server 2014](http://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx).  
  
-   Vea el tema de wiki de Technet, [solución de problemas de las instalaciones de PowerPivot (y otros complementos)](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx).  
  
## <a name="issues"></a>Problemas  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>Las imágenes en miniatura de la galería de PowerPivot se muestran como una X roja  
 Una posible causa es la **características de PowerPivot para colecciones de sitios** no está activa. Haga lo siguiente:  
  
1.  En la biblioteca de galería de PowerPivot, haga clic en **configuración del sitio** desde el icono de engranaje ![configuración de SharePoint](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "configuración de SharePoint") o **principal** lista.  
  
2.  En la sección **Administración de la colección de sitios** , haga clic en **Características de la colección de sitios**.  
  
3.  Haga clic en **Características de la colección de sitios**.  
  
4.  Comprobar **características de PowerPivot para colecciones de sitios** es **Active**.  
  
 Para otras causas de este problema, consulte [rojas para los iconos de muestra de la Galería de PowerPivot](http://support.microsoft.com/kb/2361559) (http://support.microsoft.com/kb/2361559).  
  
  
