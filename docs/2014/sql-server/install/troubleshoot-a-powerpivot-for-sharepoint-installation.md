---
title: Solucionar problemas de una instalación de PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e078becc9267c84fe139a151a15f9f67050161a8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85035853"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Solucionar problemas de una instalación de PowerPivot para SharePoint
  Si obtiene errores en lugar de las páginas y características que espera, haga lo siguiente.  
  
-   Revise las notas de la versión para SharePoint y [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con el fin de conocer soluciones alternativas para los problemas de instalación conocidos. Las notas de la versión se proporcionan con los discos de instalación o en el sitio de Microsoft del que descargó el software.  
  
    -   [SQL Server notas](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx)de la versión de 2014.  
  
-   Vea el tema de la wiki [de TechNet sobre cómo solucionar problemas de instalaciones de PowerPivot (y otros complementos)](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx).  
  
## <a name="issues"></a>Issues  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>Las imágenes en miniatura de la galería de PowerPivot se muestran como una X roja  
 Una posible causa es que la **integración de las características de PowerPivot para las colecciones de sitios** no esté activa. Haga lo siguiente:  
  
1.  En la biblioteca de la galería de PowerPivot, haga clic en **configuración del sitio** desde el icono de engranaje ![configuración de SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Configuración de SharePoint") o desde la lista **Inicio** .  
  
2.  En la sección **Administración de la colección de sitios** , haga clic en **Características de la colección de sitios**.  
  
3.  Haga clic en **Características de la colección de sitios**.  
  
4.  Compruebe que la **integración de las características de PowerPivot para las colecciones de sitios** está **activa**.  
  
 Para otras causas de este problema, vea [la galería de PowerPivot muestra X roja para iconos](https://support.microsoft.com/kb/2361559) ( https://support.microsoft.com/kb/2361559) .  
  
  
