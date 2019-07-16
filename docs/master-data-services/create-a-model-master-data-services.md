---
title: Crear un modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], creating models
- creating models [Master Data Services]
ms.assetid: 9bb3b3b3-bde8-44aa-ad62-eaae21188141
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 96eb620a89fc9f7507f194539d9c1e3e09fc169c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906652"
---
# <a name="create-a-model-master-data-services"></a>Crear un modelo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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
  
     Para reemplazar la configuración del sistema sin quitar los datos del registro de transacciones, seleccione **NO**. Para conservar solo los datos de registro de hoy y truncar los de todos los días anteriores, seleccione **SÍ** y establezca el campo **Días** en 0. Para conservar los datos de registro durante un número especificado de días, seleccione **Sí** y establezca el campo **Días** en el número de días.  
  
7.  Si lo desea, active **Crear entidad con el mismo nombre que el modelo** para crear una entidad con el mismo nombre que el modelo.  
  
8.  Haga clic en **Guardar modelo**.  
  
 Por cada modelo creado, se agrega una fila con ocho columnas a la cuadrícula. Las ocho columnas son:  
  
-   **Estado**: el estado del modelo. Al hacer clic en el botón **Guardar modelo**, se muestra la imagen ![Actualizar](../master-data-services/media/mds-model-status-updating.png "Actualizar"), que indica que se está actualizando el modelo. Si hay errores al crear o editar un modelo, se muestra la imagen ![Error](../master-data-services/media/mds-model-status-error.png "Error"). De lo contrario, el estado es correcto y se muestra la imagen ![Aceptar](../master-data-services/media/mds-model-status-ok.png "Aceptar") .  
  
-   **Nombre**: Nombre del modelo.  
  
-   **Descripción**: La descripción del modelo.  
  
-   **Días de retención del registro**: el número de días que se conserva el registro para el modelo.  
  
-   **Creado por**: el nombre del usuario que ha creado el modelo.  
  
-   **Fecha y hora de creación**: fecha y hora en que se ha creado el modelo.  
  
-   **Actualizada por**: nombre del usuario que ha actualizado el modelo por última vez.  
  
-   **Fecha y hora de actualización**: fecha y hora en que se actualizó el modelo por última vez.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Crear una entidad &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)   
 [Eliminar un modelo &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [Editar modelo &#40;Master Data Services&#41;](../master-data-services/edit-model-master-data-services.md)   
 [Transacciones &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
  
