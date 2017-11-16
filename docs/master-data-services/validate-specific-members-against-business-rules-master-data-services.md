---
title: "Validar miembros específicos con las reglas de negocios (Master Data Services) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69010f902b98ebdcb3fe1ad0f503e276ed64c08f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>Validar miembros específicos con las reglas de negocios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], aplique las reglas de negocios selectivamente si desea actualizar o validar subconjuntos de miembros con las reglas de negocios.  
  
> [!NOTE]  
>  Si quiere aplicar reglas de negocios a todos los miembros en una versión de un modelo, consulte [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Como mínimo, debe tener el permiso **Actualizar** para el objeto de modelo al que vaya a aplicar reglas de negocios.  
  
### <a name="to-apply-business-rules-selectively"></a>Aplicar reglas de negocios selectivamente  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista desplegable **Modelo** , seleccione un modelo.  
  
2.  En la lista desplegable **Versión** , seleccione una versión.  
  
3.  Haga clic en la pestaña **Explorador** .  
  
4.  En la barra de menús, seleccione **Entidades** y haga clic en el nombre de la entidad que contenga los miembros a los que desea aplicar reglas.  
  
5.  Haga clic en **Aplicar reglas**. Las reglas de negocios solo se aplican a los miembros que aparecen en la cuadrícula.  
  
## <a name="see-also"></a>Vea también  
 [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
