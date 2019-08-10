---
title: Solucionar problemas de una instalación de PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 797405386e8a6c0b9e62328699f3a73a6d845313
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892443"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Solucionar problemas de una instalación de PowerPivot para SharePoint
  Si obtiene errores en lugar de las páginas y características que espera, haga lo siguiente.  
  
-   Revise las notas de la versión para SharePoint y [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con el fin de conocer soluciones alternativas para los problemas de instalación conocidos. Las notas de la versión se proporcionan con los discos de instalación o en el sitio de Microsoft del que descargó el software.  
  
    -   [Notas de la versión de SQL Server 2014](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx).  
  
-   Vea el tema de la wiki [de TechNet sobre cómo solucionar problemas de instalaciones de PowerPivot (y otros complementos)](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx).  
  
## <a name="issues"></a>Problemas  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>Las imágenes en miniatura de la galería de PowerPivot se muestran como una X roja  
 Una posible causa es que la **integración de las características de PowerPivot para las colecciones de sitios** no esté activa. Haga lo siguiente:  
  
1.  En la biblioteca de la galería de PowerPivot, haga clic en **configuración del sitio** desde el icono de engranaje ![configuración]de SharePoint configuración de(https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint") o en la lista **Inicio** .  
  
2.  En la sección **Administración de la colección de sitios** , haga clic en **Características de la colección de sitios**.  
  
3.  Haga clic en **Características de la colección de sitios**.  
  
4.  Compruebe que la **integración de las características de PowerPivot para las colecciones de sitios** está **activa**.  
  
 Para otras causas de este problema, vea [la galería de PowerPivot muestra X roja para iconos](https://support.microsoft.com/kb/2361559) (https://support.microsoft.com/kb/2361559).  
  
  
