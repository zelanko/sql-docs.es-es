---
title: Crear un modelo (Master Data Services) | Microsoft Docs
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
- models [Master Data Services], creating models
- creating models [Master Data Services]
ms.assetid: 9bb3b3b3-bde8-44aa-ad62-eaae21188141
caps.latest.revision: 13
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 1a32cc8f778496f5609d44c17b69623b75b8c240
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="create-a-model-master-data-services"></a>Crear un modelo (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree un modelo para contener los objetos de modelo.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-model"></a>Para crear un modelo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Vista de modelo** , en la barra de menús, seleccione **Administrar** y haga clic en **Modelos**.  
  
3.  En la página **Administrar modelos** , haga clic en **Agregar**. Un panel se muestra en el lado derecho.  
  
4.  En el cuadro **Nombre** , escriba el nombre del modelo.  
  
5.  Opcionalmente, en el campo **Descripción** , escriba la descripción del modelo.  
  
6.  En el campo **Log Retention Days** (Días de retención del registro), seleccione una de las opciones de retención de datos de registro. El valor predeterminado es **Configuración del sistema**, lo que indica que el valor se hereda de la configuración del sistema del [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
     Para reemplazar la configuración del sistema sin quitar los datos del registro de transacciones, seleccione **NO**. Para conservar solo los datos de registro de hoy y truncar los datos de registro de todos los días anteriores, seleccione **SÍ** y establezca el campo **Días** en 0. Para conservar los datos de registro durante un número especificado de días, seleccione **Sí** y establezca el campo **Días** en el número de días.  
  
7.  Si lo desea, active **Crear entidad con el mismo nombre que el modelo** para crear una entidad con el mismo nombre que el modelo.  
  
8.  Haga clic en **Guardar modelo**.  
  
 Por cada modelo creado, se agrega una fila con ocho columnas a la cuadrícula. Las ocho columnas son:  
  
-   **Estado**: el estado del modelo. Al hacer clic en el botón **Guardar modelo**, se muestra la imagen ![Actualizar](../master-data-services/media/mds-model-status-updating.png "Actualizar"), que indica que se está actualizando el modelo. Si hay errores al crear o editar un modelo, se muestra la imagen ![Error](../master-data-services/media/mds-model-status-error.png "Error"). De lo contrario, el estado es correcto y se muestra la imagen ![Aceptar](../master-data-services/media/mds-model-status-ok.png "Aceptar") .  
  
-   **Nombre**: el nombre del modelo.  
  
-   **Descripción**: la descripción del modelo.  
  
-   **Días de retención del registro**: el número de días que se conserva el registro para el modelo.  
  
-   **Creado por**: el nombre del usuario que creó el modelo.  
  
-   **Fecha y hora de creación**: la fecha y hora de creación del modelo.  
  
-   **Actualizado por**: el nombre del último usuario que actualizó el modelo.  
  
-   **Fecha y hora de actualización**: la fecha y hora de la última actualización del modelo.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Crear una entidad &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)   
 [Eliminar un modelo &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [Editar modelo &#40;Master Data Services&#41;](../master-data-services/edit-model-master-data-services.md)   
 [Transacciones &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
  

