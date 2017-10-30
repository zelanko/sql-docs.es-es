---
title: "Aprobación o rechazo de un conjunto de cambios (Master Data Services) | Microsoft Docs"
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
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 849e543ec67ea42dfbed2f8138e244ede56085e5
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="approve-or-reject-a-changeset-master-data-services"></a>Aprobación o rechazo de un conjunto de cambios (Master Data Services)
  Un conjunto de cambios es una colección de cambios pendientes en los datos maestros. Si los cambios de entidad requieren la aprobación del administrador y se envía un conjunto de cambios para su aprobación, puede revisarlos y luego aprobar o rechazar el conjunto de cambios.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** . Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Debe tener permiso de administrador para la entidad.  
  
-   Para los cambios de entidad se necesita la aprobación del administrador.  
  
-   Si el estado del conjunto de cambios es pendiente, puede revisarlo y luego aprobarlo o rechazarlo.  
  
-   No se permite a los usuarios aprobar sus propios cambios. Si usted es el administrador de la entidad, debe asignar un administrador secundario para aprobar su propio conjunto de cambios.  
  
## <a name="to-approve-or-reject-a-changeset"></a>Para aprobar o rechazar un conjunto de cambios  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , seleccione el modelo y la versión y luego haga clic en **Explorador**.  
  
2.  Haga clic en una entidad en el menú **Entidades** .  
  
3.  En el panel derecho, seleccione **Conjuntos de cambios** y haga doble clic en el conjunto de cambios que quiera aprobar o rechazar.  
  
4.  Haga clic en **Aplicar** para aplicar el conjunto de cambios y revisar los cambios pendientes.  
  
5.  Haga clic en **Rechazar** para rechazar el conjunto de cambios y enviarlo de vuelta al propietario.  
  
6.  Haga clic en **Aprobar** para aprobar el conjunto de cambios. El conjunto de cambios se confirma automáticamente.  
  
## <a name="see-also"></a>Vea también  
 [Creación de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Aplicar y actualizar un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Confirmación o envío de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  

