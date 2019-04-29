---
title: Crear un grupo de atributos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 055c02ae541ec62d0ea556a20aab5d12d9c0a001
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925063"
---
# <a name="create-an-attribute-group-master-data-services"></a>Crear un grupo de atributos (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree grupos de atributos cuando desee mostrar los atributos en pestañas individuales en la cuadrícula **Explorador** .  
  
> [!NOTE]  
>  Cuando se crea un grupo de atributos, se oculta automáticamente para todos los usuarios excepto para la persona que lo creó. Para obtener más información sobre cómo hacer visible el grupo, consulte [Hacer que un grupo de atributos sea visible para los usuarios &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
-   Por lo menos debe existir un atributo. Para obtener más información, consulte [Crear un atributo de texto &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-create-an-attribute-group"></a>Para crear un grupo de atributos  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En el **vista de modelo** página, en la barra de menús, seleccione **administrar** y haga clic en **grupos de atributos**.  
  
3.  En la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Entidad** , seleccione una entidad.  
  
5.  Haga clic en **Grupos hoja**, **Grupos consolidados**o **Grupos de colecciones** para crear un grupo de atributos para los miembros hoja, los miembros consolidados o las colecciones, respectivamente.  
  
6.  Haga clic en **Agregar grupo de atributos**.  
  
7.  En el **nombre de grupo hoja** , escriba un nombre para el grupo. Este es el nombre que se muestra en la pestaña **Explorer**.  
  
    > [!NOTE]  
    >  Si seleccionó **grupos consolidados** o **grupos de colecciones** en el paso 5, esta casilla está **nombre del grupo consolidado** o **el nombre del grupo de recopilación**, respectivamente.  
  
8.  Haga clic en **Guardar grupo**.  
  
9. Expanda la carpeta del grupo.  
  
10. Haga clic en **Atributos**.  
  
11. Haga clic en **Editar elemento seleccionado**.  
  
12. Haga clic en atributos en el **disponible** y haga clic en el **agregar** flecha. Para agregarlos todos, haga clic en la flecha **Agregar todo** .  
  
13. Si lo desea, haga clic en el **seguridad** y **abajo** flechas para cambiar el orden de izquierda a derecha de los atributos.  
  
14. Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Hacer que un grupo de atributos sea visible para los usuarios &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Grupos de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [Cambiar el nombre de un grupo de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [Eliminar un grupo de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-group-master-data-services.md)   
 [Permisos de hoja &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [Consolidado permisos &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  
