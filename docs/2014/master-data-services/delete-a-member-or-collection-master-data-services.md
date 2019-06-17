---
title: Eliminar un miembro o una colección (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f3164bca23e709fd434c6ba7850ec21179a076ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479716"
---
# <a name="delete-a-member-or-collection-master-data-services"></a>Eliminar un miembro o una colección (Master Data Services)
  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], elimine un miembro o recopilación cuando ya no lo necesite. Si desea eliminar miembros de forma masiva, utilice el proceso de almacenamiento provisional en su lugar. Para obtener más información, consulte [desactivar o eliminar miembros usando el proceso de ensayo &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md).  
  
> [!NOTE]  
>  No puede eliminar un miembro si se utiliza como un valor de atributo basado en dominio para otro miembro.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Para los miembros, debe tener un mínimo de **actualización** permiso para el objeto de modelo de hoja que vaya a eliminar un miembro.  
  
-   Para las colecciones, debe tener como mínimo el permiso **Actualizar** en el objeto de colección hoja que vaya a eliminar.  
  
### <a name="to-delete-a-member-or-collection"></a>Para eliminar un miembro o colección  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista **Modelo** , seleccione un modelo.  
  
2.  En la lista **Versión** , seleccione una versión.  
  
3.  Haga clic en **Explorador**.  
  
4.  Para eliminar:  
  
    -   Un miembro hoja, en la barra de menús, seleccione **Entidades** y haga clic en el nombre de la entidad que contenga el miembro.  
  
    -   Un miembro consolidado, en la barra de menús, seleccione **Jerarquías** y haga clic en el nombre de la entidad que contenga el miembro. Después, haga clic en el nodo de la jerarquía que contiene el miembro.  
  
    -   Una colección, en la barra de menús, elija **Colecciones** y haga clic en el nombre de la entidad que contenga la colección.  
  
5.  En la cuadrícula, haga clic en la fila correspondiente al miembro o colección que desea eliminar.  
  
6.  Haga clic en **Eliminar miembro**, en **Eliminar**o en **Eliminar colección**.  
  
7.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Reactivar un miembro o una colección &#40;Master Data Services&#41;](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [Miembros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Colecciones &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md)  
  
  
