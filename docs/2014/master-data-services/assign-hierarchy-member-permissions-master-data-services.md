---
title: Asignar los permisos de los miembros de una jerarquía (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], assigning member permissions
- members [Master Data Services], assigning permissions
ms.assetid: e1b8b46a-7cd1-4a7d-9345-dd7df081e145
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b454a152eac9a61edafeaf02e30fd18f351c9daa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62926194"
---
# <a name="assign-hierarchy-member-permissions-master-data-services"></a>Asignar los permisos de los miembros de una jerarquía (Master Data Services)
  Asigne los permisos a los miembros de la jerarquía para proporcionar a los usuarios o grupos acceso para ver los datos en el área funcional del **Explorador** de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Los permisos de los miembros de la jerarquía son opcionales. Proporcionan una granularidad agregada para los permisos de objetos de modelo, que son obligatorios.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-assign-hierarchy-member-permissions"></a>Asignar los permisos de los miembros de una jerarquía  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Permisos de usuario y de grupo**.  
  
2.  En la página **Usuarios** o **Grupos** , seleccione la fila para el usuario o grupo que desea modificar.  
  
3.  Haga clic en **Editar usuario seleccionado**.  
  
4.  Haga clic en la pestaña **Miembros de la jerarquía** .  
  
5.  En la lista **Modelo** , seleccione un modelo.  
  
6.  En la lista **Versión** , seleccione una versión.  
  
7.  En la lista **Jerarquía** , seleccione una jerarquía.  
  
8.  Haga clic en **Editar**.  
  
9. Expanda el árbol y haga clic en el nodo de la jerarquía al que desea asignar los permisos.  
  
10. En el menú, seleccione **de sólo lectura**, **actualización**, o **Deny**.  
  
11. Haga clic en **Guardar**.  
  
    > [!NOTE]  
    >  Los permisos de los miembros de la jerarquía no surten efecto inmediatamente. Consulte [Aplicar inmediatamente los permisos de los miembros &#40;Master Data Services&#41;](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md) para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Eliminar los permisos de los miembros de una jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/delete-hierarchy-member-permissions-master-data-services.md)   
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permisos de miembros de la jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
