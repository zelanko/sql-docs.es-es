---
title: Eliminar usuarios o grupos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0114aa3ca6f6744303c3053003a622185d33f547
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479901"
---
# <a name="delete-users-or-groups-master-data-services"></a>Eliminar usuarios o grupos (Master Data Services)
  Elimine los usuarios o los grupos que ya no desee que tengan acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Tenga en cuenta el siguiente comportamiento al eliminar usuarios y grupos:  
  
-   Si elimina a un usuario que sea miembro de un grupo con acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], el usuario todavía puede tener acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] hasta que quite al usuario del grupo local o de Active Directory.  
  
-   Si elimina un grupo, todos los usuarios del mismo que hayan obtenido acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] se mostrarán en la lista **Usuarios** hasta que los elimine.  
  
-   Los cambios de seguridad no se propagan al sistema MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] durante 20 minutos.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-users-or-groups"></a>Eliminar usuarios o grupos  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Permisos de usuario y de grupo**.  
  
2.  Para eliminar un usuario, permanezca en la página **Usuarios** . Para eliminar un grupo, en la barra de menús, haga clic en **ManageGroups.**  
  
3.  En la cuadrícula, seleccione la fila del usuario o grupo que quiere eliminar.  
  
4.  Haga clic en **Eliminar usuario seleccionado** o en **Eliminar grupo seleccionado**.  
  
5.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Consulte también  
 [Master Data Services de &#40;de seguridad&#41;](../../2014/master-data-services/security-master-data-services.md)  
  
  
