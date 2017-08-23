---
title: Crear un administrador de entidad (Master Data Services) | Documentos de Microsoft
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
ms.assetid: 717be1e8-488e-4219-8d1e-ca9084b864cd
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e26187fb7d92fcbae23646b92d6cf02ee5511f5e
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="create-an-entity-administrator-master-data-services"></a>Creación de un administrador de entidades (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree un administrador de entidades si desea que un grupo o usuario tengan todos los permisos para todos los objetos de una o varias entidades o tengan el permiso para aprobar los conjuntos de cambios pendientes.  
  
> [!TIP]  
>  Para simplificar la administración, cree un grupo local o de Windows, y configúrelo como administrador de entidades. Puede agregar usuarios al grupo y quitarlos a continuación sin tener acceso a [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
## <a name="to-create-an-entity-administrator"></a>Para crear un administrador de entidades  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Permisos de usuario y de grupo**.  
  
2.  Seleccione la fila del usuario o grupo que desea editar y luego haga clic en **Editar usuario seleccionado**.  
  
3.  Haga clic en la pestaña **Modelos** ; también puede seleccionar un modelo de la lista **Modelos** y luego hacer clic en **Editar**.  
  
4.  Haga clic en la entidad a la que quiere conceder permisos y luego haga clic en **Admin** en el menú.  
  
5.  Realice el paso 4 con cada entidad de la que desea que el grupo o usuario sea administrador.  
  
6.  Haga clic en **Guardar**.  
  
## <a name="see-also"></a>Vea también  
 [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [Asignar permisos de objeto de modelo &#40; Master Data Services &#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Asignar permisos de miembro de jerarquía &#40; Master Data Services &#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Permisos de objeto de modelo &#40; Master Data Services &#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Permisos de miembro de jerarquía &#40; Master Data Services &#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
