---
title: "Validar miembros específicos con las reglas de negocios (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06df59d82a68c708ebb97ae82a936c88e3968011
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>Validar miembros específicos con las reglas de negocios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], aplique las reglas de negocios selectivamente si desea actualizar o validar subconjuntos de miembros con las reglas de negocios.  
  
> [!NOTE]  
>  Si quiere aplicar reglas de negocios a todos los miembros en una versión de un modelo, consulte [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Como mínimo, debe tener el permiso **Actualizar** para el objeto de modelo al que vaya a aplicar reglas de negocios.  
  
### <a name="to-apply-business-rules-selectively"></a>Aplicar reglas de negocios selectivamente  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista desplegable **Modelo** , seleccione un modelo.  
  
2.  En la lista desplegable **Versión** , seleccione una versión.  
  
3.  Haga clic en la pestaña **Explorador** .  
  
4.  En la barra de menús, seleccione **Entidades** y haga clic en el nombre de la entidad que contenga los miembros a los que desea aplicar reglas.  
  
5.  Haga clic en **Aplicar reglas**. Las reglas de negocios solo se aplican a los miembros que aparecen en la cuadrícula.  
  
## <a name="see-also"></a>Ver también  
 [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
