---
title: Permisos de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 733827ecace64ef86b54831f63fd8c2889203919
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65478964"
---
# <a name="model-permissions-master-data-services"></a>Permisos de modelo (Master Data Services)
  Los permisos de modelo se aplican a todas las entidades, jerarquías derivadas, jerarquías explícitas y colecciones dentro del modelo. Los permisos asignados al modelo se pueden invalidar con respecto a cualquier objeto individual.  
  
> [!NOTE]  
>  Si un usuario es administrador de un modelo, el modelo se muestra en todas las áreas funcionales de la interfaz de usuario. De lo contrario, el modelo solo se mostrará en el área funcional del **Explorador** . Para obtener más información, vea [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Solo lectura**|En el **Explorador**, se muestra el modelo, pero el usuario no puede Agregar o quitar miembros, y no puede actualizar los valores de atributo, pertenencias a jerarquías o pertenencias a colecciones.|  
|**Actualizar**|En el **Explorador**, se muestra el modelo y el usuario puede Agregar y quitar miembros, puede actualizar valores de atributo, pertenencias a jerarquías y pertenencias a colecciones.|  
|**Deny**|El modelo no aparece.|  
  
 Cuando asigna permisos a un modelo, el usuario obtiene acceso a todas las versiones del modelo. No puede asignar el permiso a una versión individual.  
  
## <a name="see-also"></a>Consulte también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permisos del objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Permisos de entidad &#40;Master Data Services&#41;](../../2014/master-data-services/entity-permissions-master-data-services.md)   
 [Permisos de colección &#40;Master Data Services&#41;](../../2014/master-data-services/collection-permissions-master-data-services.md)  
  
  
