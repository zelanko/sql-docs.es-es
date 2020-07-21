---
title: Permisos de miembros de la jerarquía (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a8a50ce407e0f9284d07a7248f08decacf434fee
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971415"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>Permisos de miembros de la jerarquía (Master Data Services)
  Los permisos de miembros de la jerarquía son opcionales y se deberían utilizar solo si se desea que un usuario tenga acceso limitado a miembros concretos. Si no asigna permisos en la pestaña **Miembros de la jerarquía** ,  permisos del usuario solo se basan en los permisos asignados en la pestaña **Modelos** .  
  
 Los permisos de los miembros de la jerarquía se asignan en la [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] interfaz de usuario (UI), en el área funcional **permisos de usuario y de grupo** en la pestaña miembros de la **jerarquía** . Estos permisos determinan a qué miembros puede tener acceso un usuario en el área funcional del **Explorador** de la interfaz de usuario.  
  
 En la pestaña **Miembros de la jerarquía** , cada jerarquía se representa como una estructura de árbol. Al asignar permiso a un nodo en el árbol, todos los elementos secundarios heredan ese permiso a menos que el permiso se asigne explícitamente en un nivel inferior.  
  
> [!NOTE]  
>  Cuando asigna permisos a un nodo de una jerarquía, se deniegan implícitamente a todos los miembros de los demás nodos del mismo nivel o de un nivel superior.  
  
 En el **Explorador**, los permisos de miembro se aplican en todas las ubicaciones donde se muestre el miembro. Por ejemplo, un miembro con permiso **de solo lectura** es de solo lectura en cualquier entidad, jerarquía y colección a las que pertenezca.  
  
 Los permisos de miembros de la jerarquía se aplican a la versión del modelo a la que los asigna y a cualquier copia futura de la versión. No se aplican a las versiones anteriores a la que los asigne.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Solo lectura**|Se muestran los miembros, pero el usuario no puede cambiarlos. El usuario tampoco puede mover los miembros en ninguna jerarquía explícita o colección a la que los miembros pertenezcan.<br /><br /> Nota: Si asigna el permiso **de solo lectura** a la **raíz**, los miembros de **raíz** son de solo lectura; sin embargo, en las jerarquías explícitas y colecciones, el usuario puede trasladar miembros a **raíz** y agregar nuevos miembros a la **raíz**.|  
|**Update**|Se muestran los miembros, pero el usuario no puede cambiarlos. El usuario también puede mover los miembros en cualquier jerarquía explícita o colección a la que los miembros pertenezcan.|  
|**Deny**|Los miembros no se muestran.|  
  
 En la pestaña **Miembros de la jerarquía** , los permisos que asigne no surtirán efecto inmediatamente. La frecuencia con la que se aplican permisos depende de la **configuración del intervalo de procesamiento de la seguridad de los miembros** en la tabla de configuración del sistema en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Puede aplicar permisos de los miembros de forma inmediata si sigue los pasos descritos en [Aplicar inmediatamente los permisos de los miembros &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md).  
  
> [!NOTE]  
>  No puede asignar los permisos de los miembros de la jerarquía a jerarquías recursivas, a jerarquías derivadas con límites explícitos y a jerarquías derivadas con niveles ocultos.  
  
## <a name="possible-overlapping-permissions"></a>Posibilidad de superposición de permisos  
 Cuando asigne permisos a miembros, es posible que deba resolver problemas debidos a la superposición de permisos.  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>Cuando un miembro pertenece a varias jerarquías  
 Dos o más jerarquías pueden contener el mismo miembro.  
  
-   Si un nodo de la jerarquía tiene asignado el permiso **Actualizar** y otro tiene asignado **solo lectura**, los miembros del nodo son de **solo lectura**.  
  
-   Si un nodo de la jerarquía tiene asignado el permiso **Actualizar** o **solo lectura** y se ha asignado a otro nodo **denegar**, no se mostrarán los miembros del nodo.  
  
## <a name="see-also"></a>Consulte también  
 [Asignar permisos de miembro de jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Cómo se determinan los permisos &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Miembros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Jerarquías &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchies-master-data-services.md)   
 [Aplicar inmediatamente los permisos de los miembros &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md)  
  
  
