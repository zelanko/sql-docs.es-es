---
title: "Confirmación o envío de un conjunto de cambios (Master Data Services) | Documentos de Microsoft"
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
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fd91aef621a480510896500070bd36e55d778d66
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>Confirmación o envío de un conjunto de cambios (Master Data Services)
  Un conjunto de cambios es una colección de cambios pendientes en los datos maestros. Si los cambios de entidad no requieren la aprobación por parte del administrador, puede confirmar el conjunto de cambios. Si los cambios de entidad requieren la aprobación por parte del administrador, puede enviar el conjunto de cambios para la aprobación.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** . Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)  
  
-   Si los cambios de entidad no requieren la aprobación por parte del administrador, puede confirmar el conjunto de cambios solamente si es el propietario de dicho conjunto y el estado del mismo es de abierto.  
  
-   Si los cambios de entidad requieren la aprobación por parte del administrador, puede enviar el conjunto de cambios para su aprobación solamente si es el propietario de dicho conjunto y el estado del mismo es de abierto o rechazado.  
  
## <a name="to-commit-a-local-changeset"></a>Para confirmar un conjunto de cambios local  
 La opción de confirmación solo está disponible para los conjuntos de cambios locales en entidades en las que el administrador de la entidad no ha habilitado la necesidad de aprobación.  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , seleccione el modelo y la versión y luego haga clic en **Explorador**.  
  
2.  Haga clic en una entidad en el menú **Entidades** .  
  
3.  En el panel derecho, seleccione **Conjuntos de cambios** y haga doble clic en el conjunto de cambios que quiera confirmar.  
  
4.  Haga clic en **Confirmar**.  
  
## <a name="to-submit-a-changeset"></a>Para enviar un conjunto de cambios  
 La opción de envío solo está disponible para los conjuntos de cambios en entidades en las que el administrador de la entidad no ha habilitado la necesidad de aprobación.  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , seleccione el modelo y la versión y luego haga clic en **Explorador**.  
  
2.  Haga clic en una entidad en el menú **Entidades** .  
  
3.  En el panel derecho, seleccione **Conjuntos de cambios** y haga doble clic en el conjunto de cambios que quiera enviar.  
  
4.  Haga clic en **Enviar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Aprobación o rechazo de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Creación de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Aplicar y actualizar un conjunto de cambios &#40; Master Data Services &#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Aprobación o rechazo de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
