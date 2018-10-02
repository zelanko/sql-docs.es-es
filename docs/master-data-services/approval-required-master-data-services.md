---
title: Aprobación necesaria (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: b475a53d-269d-49f3-bb42-965c555f80be
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4a7865fd7a7cd887ea8ea9dd763a2fca5d2fcc4c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612243"
---
# <a name="approval-required-master-data-services"></a>Aprobación necesaria (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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
  
  
