---
title: "Permisos de colección (Master Data Services) | Documentos de Microsoft"
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
- collections [Master Data Services], permissions
- permissions [Master Data Services], collections
ms.assetid: 703e1bf5-4b4b-4830-8a5b-f979b09f677d
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6361881ec6af124d7bbfd6cb4b4b225259823a06
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="collection-permissions-master-data-services"></a>Permisos de colección (Master Data Services)
  Los permisos de colección se aplican a todas las colecciones de una entidad. No puede conceder permisos a una colección específica; los permisos se aplican a todas las colecciones.  
  
> [!NOTE]  
>  Estos permisos solo se aplican al área funcional del **Explorador** de la interfaz de usuario.  
  
|Permiso|Description|  
|----------------|-----------------|  
|**Lectura**|El usuario puede leer los miembros de las colecciones y los atributos de los miembros.|  
|**Crear**|El usuario puede crear miembros de colecciones y asignar valores de atributos.|  
|**Update**|El usuario puede actualizar los miembros de las colecciones, así como los atributos y relaciones.|  
|**Delete**|El usuario puede eliminar miembros de colecciones.|  
|**Denegar**|Denegar todo el acceso a los miembros de las colecciones.|  
  
 Los permisos de lectura, creación, actualización y eliminación se pueden combinar. Cuando se asignan Crear, Actualizar y Eliminar, el permiso de lectura se asigna automáticamente.  
  
## <a name="see-also"></a>Vea también  
 [Asignar permisos de objeto de modelo &#40; Master Data Services &#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Colecciones de &#40; Master Data Services &#41;](../master-data-services/collections-master-data-services.md)   
 [Permisos de objeto de modelo &#40; Master Data Services &#41;](../master-data-services/model-object-permissions-master-data-services.md)  
  
  
