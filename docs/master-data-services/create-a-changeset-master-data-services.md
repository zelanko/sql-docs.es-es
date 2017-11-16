---
title: "Creación de un conjunto de cambios (Master Data Services) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cfad6f1c-9125-4896-b5f5-a4b9f9593cc4
caps.latest.revision: "9"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d2bd40bbb080a1f937735628d3ed21ddd36a5501
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-changeset-master-data-services"></a>Creación de un conjunto de cambios (Master Data Services)
  Un conjunto de cambios es una colección de cambios pendientes en los datos maestros. Si la entidad requiere aprobación para cambios, los cambios pendientes deben guardarse en un conjunto de cambios y luego enviarse para su aprobación por parte del administrador.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe disponer de permiso de acceso al área funcional Explorador. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)  
  
-   Debe tener al menos acceso de lectura a la entidad o a uno de sus atributos.  
  
## <a name="to-create-a-local-changeset"></a>Para crear un conjunto de cambios local  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , seleccione el modelo y la versión y luego haga clic en **Explorador**.  
  
2.  Haga clic en una entidad en el menú **Entidades** .  
  
3.  En el panel derecho, seleccione **Conjuntos de cambios** y haga clic en **Crear**.  
  
4.  Escriba un nombre para el conjunto de cambios y haga clic en **Guardar**.  
  
     El nombre del conjunto de cambios debe ser único dentro de un modelo.  
  
## <a name="to-create-a-changeset-for-approval"></a>Para crear un conjunto de cambios para aprobar  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , seleccione el modelo y la versión y luego haga clic en **Explorador**.  
  
2.  Haga clic en una entidad en el menú **Entidades** .  
  
3.  Realice cambios en la entidad y haga clic en**Aceptar**.  
  
4.  **Choose A changeset** (Elegir un conjunto de cambios).  
  
5.  Haga clic en **Nuevo**, escriba un nombre para el conjunto de cambios y haga clic en **Guardar**. El nombre del conjunto de cambios debe ser único dentro de un modelo.  
  
6.  Para utilizar un conjunto de cambios existente, haga clic en **Existente** y elija el conjunto de cambios en la lista. Solo están disponibles aquellos conjuntos de cambios que se encuentran en un estado de abierto o rechazado.  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Aplicar y actualizar un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Confirmación o envío de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [Aprobación o rechazo de un conjunto de cambios &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
