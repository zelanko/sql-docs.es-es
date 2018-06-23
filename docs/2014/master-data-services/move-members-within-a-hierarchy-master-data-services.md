---
title: Mover miembros dentro de una jerarquía (Master Data Services) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d5e8bf5a041458614422b3c89666ea3ffc9f5a86
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112930"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>Mover miembros dentro de una jerarquía (Master Data Services)
  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], mueva los miembros de una jerarquía para cambiar su ubicación o su asignación principal.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Para las jerarquías explícitas, debe tener un mínimo de **actualización** permiso a la entidad.  
  
-   Para las jerarquías derivadas, debe tener un mínimo de **actualización** al modelo y a todos los atributos basados en dominio utilizados en la jerarquía.  
  
### <a name="to-move-members-within-a-hierarchy"></a>Mover miembros dentro de una jerarquía  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista **Modelo** , seleccione un modelo.  
  
2.  En la lista **Versión** , seleccione una versión.  
  
3.  Haga clic en **Explorador**.  
  
4.  En la barra de menús, seleccione **jerarquías** y haga clic en *hierarchy_name*.  
  
5.  En el **jerarquía** panel, donde se muestra la jerarquía en una estructura de árbol, haga clic en la casilla de verificación para cada miembro que desee mover.  
  
6.  En la parte superior de la **jerarquía** panel, haga clic en **cortar**.  
  
7.  En el **jerarquía** panel, haga clic en la casilla de verificación para el miembro que desea mover los miembros.  
  
8.  Haga clic en **pegar**.  
  
    > [!NOTE]  
    >  En las jerarquías derivadas, sólo puede mover los miembros al mismo nivel. Asimismo, puede cambiar el criterio de ordenación de los miembros.  
  
## <a name="see-also"></a>Vea también  
 [Mover miembros de jerarquía explícita mediante el proceso de almacenamiento provisional &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Jerarquías derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [Jerarquías explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  