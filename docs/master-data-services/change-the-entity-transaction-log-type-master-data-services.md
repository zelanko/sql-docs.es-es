---
title: Cambio del tipo de registro de transacciones de entidad (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 75250b32-3384-43c2-9b5c-1607cc3aa7b3
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d981976b5a8e73ade7063c73eafb1d7a1b9dcd45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-entity-transaction-log-type-master-data-services"></a>Cambio del tipo de registro de transacciones de entidad (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Puede cambiar el tipo de registro de transacciones de una entidad, atributo, miembro o ninguno.  
  
|Tipo de registro de transacciones|Description|  
|--------------------------|-----------------|  
|Attribute|Los registros de cambio de la entidad se guardan a nivel de atributo.<br /><br /> El registro de transacciones se guarda, como para [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].|  
|Miembro|Los registros de cambio de la entidad se guardan a nivel de fila.<br /><br /> Cualquier cambio de atributo desencadena una nueva revisión de la fila.<br /><br /> Al usar el tipo de registro de transacciones de fila, la entidad se almacena como una dimensión de variación lenta de tipo 4. Se admiten la vista de suscripción tipo 2 y la vista de suscripción tipo 4 (historial). Para obtener más información, consulte [Formatos de vista de suscripciones &#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)<br /><br /> Proporciona mayor rendimiento.|  
|None|No se guardan registros de cambios.<br /><br /> Ofrece el rendimiento máximo.|  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe tener permiso de acceso al área funcional de Administración del sistema. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   La entidad debe existir. Para obtener más información, consulte [Crear una entidad &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
 **Para cambiar el tipo de registro de transacciones**  
  
1.  En Master Data Manager, haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione la fila correspondiente al modelo que contiene la entidad que desea editar y luego haga clic en **Entities**(Entidades).  
  
3.  En la página **Manage Entity** (Administrar entidad), seleccione la fila correspondiente a la entidad que quiere actualizar y luego haga clic en **Edit**(Editar).  
  
4.  Elija el tipo de registro de transacciones en la lista desplegable.  
  
5.  Haga clic en **Guardar**.  
  
  
