---
title: Eliminar los permisos de los miembros de una jerarquía (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1562bc5d71bdf873c7be1f01a1dbf48fe85c05a5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950553"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>Eliminar los permisos de los miembros de una jerarquía (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], elimine los permisos del objeto de modelo para quitar las asignaciones que se hayan realizado.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-hierarchy-member-permissions"></a>Eliminar los permisos de los miembros de una jerarquía  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Permisos de usuario y de grupo**.  
  
2.  En la página **Usuarios** o **Grupos** , seleccione la fila para el usuario o grupo que desea modificar.  
  
3.  Haga clic en **Editar usuario seleccionado**.  
  
4.  Haga clic en la pestaña **Miembros de la jerarquía** .  
  
5.  En la lista **Modelo** , seleccione un modelo.  
  
6.  En la lista **Versión** , seleccione una versión.  
  
7.  En el panel **Resumen de permisos de miembros** de la jerarquía, seleccione la fila correspondiente al permiso que desea eliminar.  
  
8.  Haga clic en **eliminar permiso seleccionado**.  
  
    > [!NOTE]  
    >  No puede quitar un permiso de un usuario si se hereda de un grupo. En su lugar debe quitar el permiso del grupo.  
  
## <a name="see-also"></a>Consulte también  
 [Permisos de miembros de la jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Asignar los permisos de los miembros de una jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
