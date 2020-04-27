---
title: Movimiento de miembros dentro de una jerarquía (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 58b39d2dc660fd51d1ba21308ff056874a239731
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054092"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>Mover miembros dentro de una jerarquía (Master Data Services)
  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], mueva los miembros de una jerarquía para cambiar su ubicación o su asignación principal.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   En el caso de las jerarquías explícitas, debe tener como mínimo el permiso **Actualizar** para la entidad.  
  
-   En el caso de las jerarquías derivadas, debe tener un mínimo de **actualización** al modelo y a cualquier atributo basado en dominio que se use en la jerarquía.  
  
### <a name="to-move-members-within-a-hierarchy"></a>Mover miembros dentro de una jerarquía  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista **Modelo** , seleccione un modelo.  
  
2.  En la lista **Versión** , seleccione una versión.  
  
3.  Haga clic en **Explorador**.  
  
4.  En la barra de menús, seleccione **jerarquías** y haga clic en *hierarchy_name*.  
  
5.  En el panel **jerarquía** , donde la jerarquía se muestra en una estructura de árbol, haga clic en la casilla de cada miembro que desee desplace.  
  
6.  En la parte superior del panel **jerarquía** , haga clic en **cortar**.  
  
7.  En el panel **jerarquía** , haga clic en la casilla correspondiente al miembro al que desea trasladar los miembros.  
  
8.  Haga clic en **pegar**.  
  
    > [!NOTE]  
    >  En las jerarquías derivadas, sólo puede mover los miembros al mismo nivel. Asimismo, puede cambiar el criterio de ordenación de los miembros.  
  
## <a name="see-also"></a>Consulte también  
 [Mueva los miembros de la jerarquía explícita mediante el proceso de almacenamiento provisional &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Jerarquías derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [Jerarquías explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
