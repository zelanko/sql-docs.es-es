---
title: Agregar un grupo (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- groups [Master Data Services], adding
- adding groups [Master Data Services]
ms.assetid: c7a88381-3b2c-4af7-9cf7-3a930c1abdee
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2398be897b1f231c2e507dc1f0960a811df3eca7
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="add-a-group-master-data-services"></a>Agregar un grupo (Master Data Services)
  Agregue un grupo a la lista **Grupos** en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] a fin de comenzar el proceso para asignar el permiso a la aplicación web. Para que un usuario del grupo pueda tener acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], debe conceder el permiso de grupo a una o más áreas funcionales, y objetos de modelo.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
### <a name="to-add-a-group"></a>Agregar un grupo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Permisos de usuario y de grupo**.  
  
2.  En la página **Usuarios** de la barra de menús, haga clic en **Administrar grupos**.  
  
3.  Haga clic en **Agregar grupos**.  
  
4.  Escriba el nombre del grupo precedido por el nombre de dominio de Active Directory o por el nombre del equipo servidor, como en *dominio\nombre_grupo* o *equipo\nombre_grupo*.  
  
5.  Si lo desea, haga clic en **Comprobar nombres**.  
  
6.  Haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  Cuando el usuario obtiene acceso por primera vez a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], su nombre se agrega a la lista de usuarios de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
## <a name="next-steps"></a>Next Steps  
  
-   [Asignar permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/assign-functional-area-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Ver también  
 [Seguridad &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
