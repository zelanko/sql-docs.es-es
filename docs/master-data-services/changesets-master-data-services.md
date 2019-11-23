---
title: Conjuntos de cambios
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f227c49a-ed46-4e0f-8992-83093456cf94
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6d8c277796f743b31dfb5df349352bb6c7470421
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728619"
---
# <a name="changesets-master-data-services"></a>Conjuntos de cambios (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] admite ahora la posibilidad de guardar los cambios pendientes en una entidad como conjuntos de cambios. Hay dos escenarios de uso para esta característica.  
  
-   **Cambios si el administrador de la entidad ha activado "Aprobación necesaria"**  
  
     Si un administrador de la entidad especifica que los cambios realizados en una entidad determinada necesitan aprobación antes de que se confirmen, los cambios realizados en la entidad deben guardarse en un conjunto de cambios nuevo o existente antes de que se puedan enviar para su aprobación.  Para obtener más información, consulte [Aprobación necesaria &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md)  
  
     Seguirá este flujo de trabajo.  
  
    1.  Cree un conjunto de cambios. El conjunto de cambios está en estado abierto. Consulte [Create a Changeset &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  Aplique el conjunto de cambios y agregue algunos cambios al conjunto de cambios. Consulte [Apply and Update a Changeset &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  Envíe el conjunto de cambios al administrador de la entidad para su aprobación. El conjunto de cambios está en estado pendiente. Consulte [Commit or Submit a Changeset &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
    4.  El administrador de la entidad recibe una notificación por correo electrónico en la que se indica que hay un conjunto de cambios esperando su aprobación. Si el administrador de la entidad aprueba el conjunto de cambios, el conjunto de cambios está en estado aprobado. Consulte [Approve or Reject a Changeset &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
    5.  El conjunto de cambios aprobado se confirmará de forma automática. Si el cambio se confirma correctamente, el conjunto de cambios está en estado confirmado.  
  
-   **Cambios de usuario local**  
  
     Si simplemente quiere guardar los cambios locales para poder usarlos o recuperarlos más adelante, puede usar conjuntos de cambios.  
  
     Seguirá este flujo de trabajo.  
  
    1.  Cree un conjunto de cambios. El conjunto de cambios está en estado abierto. Consulte [Create a Changeset &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  Aplique el conjunto de cambios y agregue algunos cambios al conjunto de cambios. Consulte [Apply and Update a Changeset &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  Cuando esté listo, confirme el conjunto de cambios. Consulte [Commit or Submit a Changeset &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Creación de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Aplicar y actualizar un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Confirmación o envío de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [Aprobación o rechazo de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)   
 [Administración de conjuntos de datos &#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md)  
  
  
