---
description: Conjuntos de cambios (Master Data Services)
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
ms.openlocfilehash: 7171e28103ebf0c18657a62a954faa1ca64cdf5a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88345022"
---
# <a name="changesets-master-data-services"></a>Conjuntos de cambios (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] admite ahora la posibilidad de guardar los cambios pendientes en una entidad como conjuntos de cambios. Hay dos escenarios de uso para esta característica.  
  
-   **Cambios cuando el administrador de la entidad activa la "aprobación requerida"**  
  
     Si un administrador de la entidad especifica que los cambios realizados en una entidad determinada necesitan aprobación antes de que se confirmen, los cambios realizados en la entidad deben guardarse en un conjunto de cambios nuevo o existente antes de que se puedan enviar para su aprobación.  Para obtener más información, consulte [Aprobación necesaria &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md)  
  
     Seguirá este flujo de trabajo.  
  
    1.  Cree un conjunto de cambios. El conjunto de cambios está en estado abierto. Consulte [Creación de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  Aplique el conjunto de cambios y agregue algunos cambios al conjunto de cambios. Consulte [Aplicar y actualizar un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  Envíe el conjunto de cambios al administrador de la entidad para su aprobación. El conjunto de cambios está en estado pendiente. Consulte [Confirmación o envío de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
    4.  El administrador de la entidad recibe una notificación por correo electrónico en la que se indica que hay un conjunto de cambios esperando su aprobación. Si el administrador de la entidad aprueba el conjunto de cambios, el conjunto de cambios está en estado aprobado. Consulte [Aprobación o rechazo de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
    5.  El conjunto de cambios aprobado se confirmará de forma automática. Si el cambio se confirma correctamente, el conjunto de cambios está en estado confirmado.  
  
-   **Cambios de usuario local**  
  
     Si simplemente quiere guardar los cambios locales para poder usarlos o recuperarlos más adelante, puede usar conjuntos de cambios.  
  
     Seguirá este flujo de trabajo.  
  
    1.  Cree un conjunto de cambios. El conjunto de cambios está en estado abierto. Consulte [Creación de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  Aplique el conjunto de cambios y agregue algunos cambios al conjunto de cambios. Consulte [Aplicar y actualizar un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  Cuando esté listo, confirme el conjunto de cambios. Consulte [Confirmación o envío de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Consulte también  
 [Crear un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Aplicar y actualizar un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Confirmar o enviar un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [Aprobar o rechazar un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)   
 [Administración de conjuntos de datos &#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md)  
  
  
