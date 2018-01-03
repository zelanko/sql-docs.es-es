---
title: "Crear y ejecutar una relación de sincronización de entidades (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0ddceab4-d2b3-4bc1-bd9c-6b852200b414
caps.latest.revision: "6"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8cd875b088c8c7003123db63b6f6584f80a93a42
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="create-and-execute-an-entity-sync-relationship-master-data-services"></a>Crear y ejecutar una relación de sincronización de entidades (Master Data Services)
  La sincronización de entidades es una sincronización unidireccional y repetible entre versiones de entidades que proporciona una forma de compartir datos de entidad entre diferentes modelos.  
  
## <a name="prerequisites"></a>Prerequisites  
 Estos son los requisitos previos para crear una relación de sincronización de entidades:  
  
-   Debe disponer de permiso para tener acceso al área funcional de Administración del sistema. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Debe ser administrador de modelo del modelo de destino. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Debe tener al menos acceso de lectura a la entidad de origen y a todos sus atributos y miembros.  
  
 Estos son los requisitos previos para ejecutar una relación de sincronización de entidades:  
  
-   Debe disponer de permiso para tener acceso al área funcional de Administración del sistema. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Debe ser administrador de modelo del modelo de destino. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 Tenga en cuenta lo siguiente al crear una relación de sincronización de entidades.  
  
-   Las entidades de origen y de destino deben estar en modelos distintos.  
  
-   El estado de una versión de entidad de destino no debe confirmarse.  
  
-   Cuando se haya establecido una relación de sincronización, el destino se sincronizará inmediatamente con el origen.  
  
-   Una versión de entidad de destino no puede ser una versión de entidad de origen en otra relación de sincronización.  
  
 Tenga en cuenta lo siguiente al ejecutar una relación de sincronización de entidades.  
  
-   Solo se copiarán los miembros hoja.  
  
-   No se copiarán los atributos basados en dominio.  
  
-   No se copiarán los miembros eliminados temporalmente.  
  
-   La sincronización no genera transacciones/historiales de entidad de destino.  
  
 **Para crear una relación de sincronización de entidades**  
  
1.  En Master Data Manager, haga clic en **Administración del sistema**.  
  
2.  En la barra de menús de la página **Vista de modelo** , seleccione **Administrar** y haga clic en **Entity Sync**(Sincronización de entidades).  
  
3.  En la página **Entity Sync Maintenance** (Mantenimiento de sincronización de entidades), haga clic en **Agregar**. Se abre un panel a la derecha.  
  
4.  En la lista **Modelo** del origen, seleccione un modelo.  
  
5.  En la lista **Versión** del origen, seleccione una versión.  
  
6.  En la lista **Entidad** del origen, seleccione una entidad.  
  
7.  En la lista **Modelo** del destino, seleccione un modelo.  
  
8.  En la lista **Versión** del destino, seleccione una versión.  
  
9. Elija **Existing Entity** (Entidad existente) y seleccione una entidad de la lista de entidades (si quiere sincronizar una entidad existente) o elija **Nueva entidad** y escriba el nombre de la entidad de destino (si quiere sincronizar con una nueva entidad).  
  
10. Seleccione **Sync On Demand**(Sincronizar a petición) o seleccione **Auto Sync** (Sincronización automática) y establezca una frecuencia.  
  
11. Haga clic en **Guardar**.  
  
 **Para ejecutar una relación de sincronización de entidades**  
  
1.  En Master Data Manager, haga clic en **Administración del sistema**.  
  
2.  En la barra de menús de la página **Vista de modelo** , seleccione **Administrar** y haga clic en **Entity Sync**(Sincronización de entidades).  
  
3.  En la página **Mantenimiento de sincronización de entidades** , seleccione una relación de sincronización en la cuadrícula.  
  
4.  Haga clic en **Ejecutar**.  
  
## <a name="sync-relationship-information"></a>Información de las relaciones de sincronización  
 Por cada relación de sincronización creada, se agrega a la cuadrícula una fila con diez columnas. En la siguiente tabla se describen las columnas.  
  
|columna|Description|  
|------------|-----------------|  
|Estado|Estado de la relación de sincronización.<br /><br /> Al hacer clic en **Guardar** o ejecutar una relación de sincronización, aparece la imagen ![Icono de estado de actualización](../master-data-services/media/mds-statusicon-updating.png "Icono de estado de actualización"), que indica que la relación de sincronización se está actualizando.<br /><br /> Si hay errores al crear, editar o ejecutar una relación de sincronización, aparecerá la imagen ![Icono de estado de error](../master-data-services/media/mds-statusicon-error.png "Icono de estado de error").<br /><br /> En caso contrario, el estado será correcto y aparecerá la imagen ![Icono de estado correcto](../master-data-services/media/mds-statusicon-ok.png "Icono de estado correcto").|  
|Modelo de origen|Nombre del modelo de origen.|  
|Versión de origen|Nombre de la versión de origen.|  
|Entidad de origen|Nombre de la entidad de origen.|  
|Modelo de destino|Nombre del modelo de destino.|  
|Versión de destino|Nombre de la versión de destino.|  
|Entidad de destino|Nombre de la entidad de destino.|  
|Frecuencia|Especifica la frecuencia de la relación de sincronización.|  
|Last Attempt Time (Hora del último intento)|Indica la hora en la que se produjo el último intento de sincronización.|  
|Last Successful Time (Hora del último intento correcto)|Indica la hora en la que se produjo el último intento de sincronización correcto.|  
  
 Cuando se hace clic en un índice, se muestra la siguiente información.  
  
-   **Last Attempt Error**(Error de último intento): muestra información de error relativa al último intento de sincronización.  
  
-   **Creado por:**nombre del usuario que creó la sincronización.  
  
-   **El:**fecha y hora en que se creó la sincronización.  
  
-   **Actualizado por:**nombre del usuario que actualizó la sincronización por última vez.  
  
-   **El:**fecha y hora en que se actualizó la sincronización por última vez.  
  
## <a name="next-steps"></a>Next Steps  
 [Modificación y eliminación de una relación de sincronización de entidades &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
