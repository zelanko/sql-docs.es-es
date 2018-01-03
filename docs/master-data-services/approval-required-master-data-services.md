---
title: "Aprobación necesaria (Master Data Services) | Microsoft Docs"
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
ms.assetid: b475a53d-269d-49f3-bb42-965c555f80be
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5fa143b8b1f8316d5de80b895399e328d8a6a6c8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="approval-required-master-data-services"></a>Aprobación necesaria (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], el administrador puede establecer una entidad en Aprobación necesaria. Todos los cambios de esta entidad requerirán que uno de los administradores de la entidad revise y apruebe los cambios.  
  
> [!NOTE]  
>  Los cambios realizados en los miembros hoja requieren aprobación. Los cambios realizados en colecciones y jerarquías explícitas en desuso omiten la aprobación.  
>   
>  Los cambios realizados por el proceso de tablas de almacenamiento provisional omiten la aprobación.  
>   
>  Los cambios realizados por una regla de negocio omiten la aprobación.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para acceder al área funcional de Administración del sistema.  
  
-   Debe ser administrador de modelo. Para obtener más información, consulte [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)  
  
-   Debe existir una entidad. Para obtener más información, consulte [Crear una entidad &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="to-enable-approval-required-for-an-entity"></a>Para habilitar la opción Aprobación necesaria para una entidad  
  
1.  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), en la cuadrícula, seleccione la fila de la entidad para la que desea habilitar  **Aprobación necesaria** .  
  
4.  Haga clic en **Editar**, seleccione **Aprobación necesaria**y luego haga clic en **Guardar**.  
  
## <a name="see-also"></a>Ver también  
 [Conjuntos de cambios &#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md)  
  
  
