---
title: Crear un administrador de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 464e82ea23aa724d84af25c69a7168f95d09afe1
ms.sourcegitcommit: 39d8d2d504d0ab70bac5ae3e981657e15dfb7bee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/10/2020
ms.locfileid: "78964368"
---
# <a name="create-a-model-administrator-master-data-services"></a>Crear un administrador de modelo (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree un administrador de modelo cuando desee que un grupo o usuario tenga el permiso **Actualizar** para todos los objetos de uno o varios modelos.  
  
> [!TIP]  
>  Para simplificar la administración, cree un grupo local o de Windows y configúrelo como administrador del modelo. Puede agregar usuarios al grupo y quitarlos a continuación sin tener acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="prerequisites"></a>Prerrequisitos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional **Permisos de usuario y de grupo** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-a-model-administrator"></a>Para crear un administrador de modelo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Permisos de usuario y de grupo**.  
  
2.  En la página **Usuarios** o **Grupos** , seleccione la fila para el usuario o grupo que desea modificar.  
  
3.  Haga clic en **Editar usuario seleccionado**.  
  
4.  Haga clic en la pestaña **Modelos** .  
  
5.  Si lo desea, seleccione un modelo en la lista desplegable **Modelo** .  
  
6.  Haga clic en **Editar**.  
  
7.  Haga clic en el modelo al que desea conceder el permiso.  
  
8.  En el menú, seleccione **Actualizar**.  
  
9. Complete los pasos 7 y 8 con cada modelo para el que desee que administren el grupo o el usuario.  
  
10. Haga clic en **Save**(Guardar).  
  
## <a name="remarks"></a>Observaciones  
 No asigne ningún otro permiso para los objetos de modelo o los miembros de la jerarquía. Si lo hace, el usuario ya no es un administrador y no puede ver el modelo en ningún área funcional que no sea el **Explorador**.  
  
 Existe una excepción: Si el usuario tiene el permiso **Actualizar** asignado a una **raíz** de jerarquía en la pestaña miembros de la **jerarquía** , el usuario se considera un administrador del modelo.  
  
## <a name="see-also"></a>Consulte también  
 [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md)   
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Asignar permisos de miembro de jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Permisos del objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Permisos de miembros de la jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
