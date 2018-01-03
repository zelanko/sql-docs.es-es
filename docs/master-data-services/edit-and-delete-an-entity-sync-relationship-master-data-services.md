---
title: "Modificación y eliminación de una relación de sincronización de entidades (Master Data Services) | Microsoft Docs"
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
ms.assetid: 9a5e37f3-352e-45a6-b4a0-6f98f83b4bd8
caps.latest.revision: "6"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: afbfa60002d96fa11d76eca3146f13117e49fd22
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="edit-and-delete-an-entity-sync-relationship-master-data-services"></a>Modificación y eliminación de una relación de sincronización de entidades (Master Data Services)
  La sincronización de entidades es una sincronización unidireccional y repetible entre versiones de entidades que proporciona una forma de compartir datos de entidad entre diferentes modelos. Puede modificar y eliminar una relación de sincronización que haya creado.  
  
## <a name="prerequisites"></a>Prerequisites  
 Requisitos previos para modificar una relación de sincronización de entidades  
  
-   Debe disponer de permiso para tener acceso al área funcional de Administración del sistema. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Debe ser administrador de modelo del modelo de destino. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Debe tener al menos acceso de lectura a la entidad de origen y a todos sus atributos y miembros.  
  
 Requisitos previos para eliminar una relación de sincronización de entidades  
  
-   Debe disponer de permiso para tener acceso al área funcional de Administración del sistema. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Debe ser administrador de modelo del modelo de destino. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 Tenga en cuenta lo siguiente al modificar una relación de sincronización de entidades.  
  
-   Las entidades de origen y de destino deben estar en modelos distintos.  
  
-   El estado de una versión de entidad de destino no debe confirmarse.  
  
-   Cuando se haya establecido una relación de sincronización, el destino se sincronizará inmediatamente con el origen.  
  
-   Una versión de entidad de destino no puede ser una versión de entidad de origen en otra relación de sincronización.  
  
 Tenga en cuenta lo siguiente al ejecutar una relación de sincronización de entidades.  
  
-   Solo se copiarán los miembros hoja.  
  
-   No se copiarán los atributos basados en dominio.  
  
-   No se copiarán los miembros eliminados temporalmente.  
  
-   La sincronización no genera transacciones/historiales de entidad de destino.  
  
 **Para modificar una relación de sincronización de entidades**  
  
1.  En Master Data Manager, haga clic en **Administración del sistema**.  
  
2.  En la barra de menús de la página **Vista de modelo** , seleccione **Administrar** y haga clic en **Entity Sync**(Sincronización de entidades).  
  
3.  En la página **Entity Sync Maintenance** (Mantenimiento de sincronización de entidades), seleccione una relación de sincronización en la cuadrícula.  
  
4.  Haga clic en **Editar**. Se abre un panel a la derecha.  
  
5.  Cambie el valor de **Frecuencia**. Seleccione **Sync On Demand**(Sincronizar a petición) o seleccione **Auto Sync** (Sincronización automática) y establezca una frecuencia.  
  
6.  Haga clic en **Guardar**.  
  
 **Para eliminar una relación de sincronización de entidades**  
  
1.  En Master Data Manager, haga clic en **Administración del sistema**.  
  
2.  En la barra de menús de la página **Vista de modelo** , seleccione **Administrar** y haga clic en **Entity Sync**(Sincronización de entidades).  
  
3.  En la página **Entity Sync Maintenance** (Mantenimiento de sincronización de entidades), seleccione una relación de sincronización en la cuadrícula.  
  
4.  Haga clic en **Eliminar**.  
  
5.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Ver también  
 [Crear y ejecutar una relación de sincronización de entidades &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Relación de sincronización de entidades &#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md)  
  
  
