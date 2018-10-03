---
title: Ocultar o eliminar niveles en una jerarquía derivada (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, hiding levels
- derived hierarchies, deleting levels
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 703e18130367c3d508cc6f40f4cdb9af17093f4e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088135"
---
# <a name="hide-or-delete-levels-in-a-derived-hierarchy-master-data-services"></a>Ocultar o eliminar niveles en una jerarquía derivada (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], oculte un nivel en una jerarquía derivada cuando requiera el nivel para agrupar, pero no necesite mostrarlo. Elimine un nivel cuando no desee usarlo para la agrupación.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-hide-or-delete-levels-in-a-derived-hierarchy"></a>Para ocultar o eliminar niveles en una jerarquía derivada  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En el **vista de modelo** página, en la barra de menús, seleccione **administrar** y haga clic en **jerarquías derivadas**.  
  
3.  En la página **Mantenimiento de jerarquías derivadas** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Seleccione la fila de la jerarquía derivada que desea modificar.  
  
5.  Haga clic en **seleccionado de Editar jerarquía derivada**.  
  
6.  En el panel **Niveles actuales** :  
  
    -   Para ocultar un nivel, haga clic en un nivel distinto de la parte superior o inferior. En la lista **Visible** , seleccione **No**. A continuación, haga clic en **Guardar elemento de jerarquía seleccionado**.  
  
    -   Para eliminar el nivel superior, haga clic en **Eliminar elemento de jerarquía seleccionado**. En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. Solo puede eliminar el nivel superior.  
  
## <a name="see-also"></a>Vea también  
 [Mover miembros dentro de una jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/move-members-within-a-hierarchy-master-data-services.md)   
 [Jerarquías derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  
