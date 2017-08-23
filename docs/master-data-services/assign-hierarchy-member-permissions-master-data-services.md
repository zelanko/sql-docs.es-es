---
title: "Asignar permisos de miembro de jerarquía (Master Data Services) | Documentos de Microsoft"
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
- permissions [Master Data Services], assigning member permissions
- members [Master Data Services], assigning permissions
ms.assetid: e1b8b46a-7cd1-4a7d-9345-dd7df081e145
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f7a7e6cafe48506446396b83200d4d2343aa7949
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="assign-hierarchy-member-permissions-master-data-services"></a>Asignar los permisos de los miembros de una jerarquía (Master Data Services)
  Asigne los permisos a los miembros de la jerarquía para proporcionar a los usuarios o grupos acceso para ver los datos en el área funcional del **Explorador** de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Los permisos de los miembros de la jerarquía son opcionales. Proporcionan una granularidad agregada para los permisos de objetos de modelo, que son obligatorios.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
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
  
10. En el menú, seleccione una combinación de permisos **Crear**, **Leer, Actualizar** y **Eliminar** , o bien permisos **Denegar** .  
  
11. Haga clic en **Guardar**.  
  
    > [!NOTE]  
    >  Los permisos de los miembros de la jerarquía no surten efecto inmediatamente. Consulte [Aplicar inmediatamente los permisos de los miembros &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md) para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Eliminar los permisos de los miembros de una jerarquía &#40;Master Data Services&#41;](../master-data-services/delete-hierarchy-member-permissions-master-data-services.md)   
 [Asignar permisos de objeto de modelo &#40; Master Data Services &#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permisos de miembro de jerarquía &#40; Master Data Services &#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
