---
title: "Permisos del área funcional (Master Data Services) | Microsoft Docs"
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
helpviewer_keywords:
- functional area permissions [Master Data Services], about functional area permissions
- functional area permissions [Master Data Services]
- permissions [Master Data Services], functional areas
ms.assetid: a80b87b3-b904-4cda-8582-0761c2617c57
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2a0fe1d27bd0ed1b70b3d31aacfca43cb291c1f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="functional-area-permissions-master-data-services"></a>Permisos del área funcional (Master Data Services)
  Puede asignar permisos a cada una de las áreas funcionales de la interfaz de usuario de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Las siguientes son las áreas funcionales:  
  
-   **Explorador**  
  
-   **Administración de versiones**  
  
-   **Administración de integraciones**  
  
-   **Administración del sistema**  
  
-   **Permisos de usuario y de grupo**  
  
-   **Superusuario.**  
  
 Cuando se asignan permisos a un área funcional, está haciendo que el área de la IU sea visible al usuario o grupo.  
  
 Dentro del área funcional del **Explorador** , los permisos adicionales asignados a los objetos de modelo y a los miembros de la jerarquía determinan a qué datos puede tener acceso un usuario. Dentro de todas las demás áreas funcionales, un usuario debe ser administrador de modelo para ver un modelo y actuar en él. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
> [!IMPORTANT]  
>  Un usuario con permisos de superusuario tiene permiso efectivo de administrador en todos los modelos y tiene todos los demás permisos funcionales.  
  
 Un usuario o grupo deben disponer de permisos para al menos un área funcional y un modelo en la pestaña **Modelos** con el fin de tener acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="see-also"></a>Ver también  
 [Asignar permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/assign-functional-area-permissions-master-data-services.md)   
 [Permisos de objeto del modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Permisos de miembros de la jerarquía &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Cómo se determinan los permisos &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
