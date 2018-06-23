---
title: Permisos de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e92f595bcf701e20378fe94dfde6c91d8c57bee1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106773"
---
# <a name="model-permissions-master-data-services"></a>Permisos de modelo (Master Data Services)
  Los permisos de modelo se aplican a todas las entidades, jerarquías derivadas, jerarquías explícitas y colecciones dentro del modelo. Los permisos asignados al modelo se pueden invalidar con respecto a cualquier objeto individual.  
  
> [!NOTE]  
>  Si un usuario es administrador de un modelo, el modelo se muestra en todas las áreas funcionales de la interfaz de usuario. De lo contrario, el modelo solo se mostrará en el área funcional del **Explorador** . Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Solo lectura**|En **Explorer**, se muestra el modelo pero el usuario no puede agregar o quitar miembros y no se puede actualizar valores de atributo, pertenencias a jerarquías o pertenencias a la colección.|  
|**Update**|En **Explorer**, se muestra el modelo y el usuario puede agregar y quitar miembros, puede actualizar los valores de atributo, pertenencias a jerarquías y miembros de la colección.|  
|**Denegar**|El modelo no aparece.|  
  
 Cuando asigna permisos a un modelo, el usuario obtiene acceso a todas las versiones del modelo. No puede asignar el permiso a una versión individual.  
  
## <a name="see-also"></a>Vea también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Permisos de entidad &#40;Master Data Services&#41;](../../2014/master-data-services/entity-permissions-master-data-services.md)   
 [Permisos de colección &#40;Master Data Services&#41;](../../2014/master-data-services/collection-permissions-master-data-services.md)  
  
  