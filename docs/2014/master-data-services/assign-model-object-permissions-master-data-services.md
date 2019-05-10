---
title: Asignar permisos de objeto de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], assigning object permissions
- permissions [Master Data Services], assigning model object permissions
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a1477f934dfa8a23fa5498124b74c9a150b24a33
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65480077"
---
# <a name="assign-model-object-permissions-master-data-services"></a>Asignar permisos de objeto de modelo (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], asigne permisos a los objetos de modelo cuando necesite proporcionar a un usuario o grupo acceso a los datos en el área funcional del **Explorador** de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]o cuando necesite convertir en administrador a un usuario o grupo.  
  
> [!NOTE]  
>  Al asignar el permiso a un modelo, implícitamente se deniega el permiso a todos los otros modelos. Si no asigna permisos del objeto de modelo, el usuario o grupo no pueden tener acceso a ningún dato en el **Explorador**.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-assign-model-object-permissions"></a>Asignar permisos de objeto de modelo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Permisos de usuario y de grupo**.  
  
2.  En la página **Usuarios** o **Grupos** , seleccione la fila para el usuario o grupo que desea modificar.  
  
3.  Haga clic en **Editar usuario seleccionado**.  
  
4.  Haga clic en la pestaña **Modelos** .  
  
5.  Si lo desea, seleccione un modelo en la lista desplegable **Modelo** .  
  
6.  Haga clic en **Editar**.  
  
7.  Expanda el árbol y haga clic en el objeto de modelo al que desea asignar los permisos.  
  
8.  En el menú, seleccione **de sólo lectura**, **actualización**, o **Deny**.  
  
9. Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   (Opcional) [Asignar los permisos de los miembros de una jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Eliminar permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/delete-model-object-permissions-master-data-services.md)   
 [Permisos de objeto del modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Crear un administrador de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-administrator-master-data-services.md)  
  
  
