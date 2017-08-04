---
title: Eliminar usuarios o grupos (Master Data Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5c0a5934afc97b24d884738aa1d6f8c2cc1c80cf
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="delete-users-or-groups-master-data-services"></a>Eliminar usuarios o grupos (Master Data Services)
  Elimine los usuarios o los grupos que ya no desee que tengan acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Tenga en cuenta el siguiente comportamiento al eliminar usuarios y grupos:  
  
-   Si elimina a un usuario que sea miembro de un grupo con acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], el usuario todavía puede tener acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] hasta que quite al usuario del grupo local o de Active Directory.  
  
-   Si elimina un grupo, todos los usuarios del mismo que hayan obtenido acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] se mostrarán en la lista **Usuarios** hasta que los elimine.  
  
-   Los cambios de seguridad no se propagan al sistema MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] durante 20 minutos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
### <a name="to-delete-users-or-groups"></a>Eliminar usuarios o grupos  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Permisos de usuario y de grupo**.  
  
2.  Para eliminar un usuario, permanezca en la página **Usuarios** . Para eliminar un grupo, en la barra de menús, haga clic en **ManageGroups.**  
  
3.  En la cuadrícula, seleccione la fila del usuario o grupo que quiere eliminar.  
  
4.  Haga clic en **Eliminar usuario seleccionado** o en **Eliminar grupo seleccionado**.  
  
5.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Seguridad &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
