---
title: Eliminar un modelo (Master Data Services) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting models [Master Data Services]
- models [Master Data Services], deleting models
ms.assetid: f0ad3cc4-aed7-47c8-94bc-2971fe9fe871
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f1ac3250d2d1f852ec43bf88fb206b2009fc0430
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="delete-a-model-master-data-services"></a>Eliminar un modelo (Master Data Services)
  Elimine un modelo para quitar el modelo y todos sus datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
> [!NOTE]  
>  Cuando haya completado este procedimiento, se eliminarán permanentemente todos los objetos y todos los datos de todas las versiones del modelo.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-a-model"></a>Eliminar un modelo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Vista de modelo** , en la barra de menús, seleccione **Administrar** y haga clic en **Modelos**.  
  
3.  En la página **Administrar modelos** , en la cuadrícula, seleccione la fila del modelo que desea eliminar.  
  
4.  Haga clic en **Eliminar**.  
  
5.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
6.  En el cuadro de diálogo de confirmación adicional, haga clic en **Aceptar**.  
  
 La columna **Estado** de la cuadrícula muestra el estado de la operación en el modelo. Al hacer clic en el botón **Guardar modelo**, se muestra la imagen ![Actualizar](../master-data-services/media/mds-model-status-updating.png "Actualizar"), que indica que se está actualizando el modelo. Si hay errores al crear o editar un modelo, se muestra la imagen ![Error](../master-data-services/media/mds-model-status-error.png "Error"). De lo contrario, el estado es correcto y se muestra la imagen ![Aceptar](../master-data-services/media/mds-model-status-ok.png "Aceptar") .  
  
## <a name="see-also"></a>Vea también  
 [Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [Crear un modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)  
  
  
