---
title: "Reactivar un miembro o una colección (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services], reactivating
- consolidated members [Master Data Services], reactivating
- reactivating members [Master Data Services]
- members [Master Data Services], reactivating
- reactivating collections [Master Data Services]
- leaf members [Master Data Services], reactivating
ms.assetid: bb4884c0-3658-4763-92d1-636804278b1c
caps.latest.revision: 11
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: acad653184afbc9207e7b408789927d929fbf355
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="reactivate-a-member-or-collection-master-data-services"></a>Reactivar un miembro o una colección (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede reactivar un miembro que:  
  
-   Se desactivó usando el proceso de almacenamiento provisional.  
  
-   Se eliminó en MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
-   Se eliminó en la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
 Al reactivar un miembro, se restauran sus atributos y su pertenencia a jerarquías y colecciones.  
  
 También puede reactivar colecciones. Cuando lo hace, se restauran los atributos y los miembros que pertenecen a la colección.  
  
 Cuando se reactiva un miembro o colección, se restauran todas las transacciones anteriores.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], debe disponer de permiso para el área funcional **Administración de versiones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-reactivate-a-member-or-collection"></a>Para reactivar un miembro o colección  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , haga clic en **Administración de versiones**.  
  
2.  En la barra de menús, haga clic en **Transacciones**.  
  
3.  En la página **Transacciones** , en la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Versión** , seleccione una versión.  
  
5.  En el panel **Transacciones** , haga clic en la fila correspondiente al miembro o colección que desea reactivar. Esta fila debe mostrar **Activo** en la columna **Valor anterior** y **Desactivado** en la columna **Nuevo valor** .  
  
6.  Haga clic en **Invertir transacción**.  
  
7.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. Se agregará una nueva transacción que muestra **Activo** en la columna **Nuevo valor** .  
  
## <a name="see-also"></a>Vea también  
 [Eliminar un miembro o una colección &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)   
 [Miembros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Colecciones &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  

