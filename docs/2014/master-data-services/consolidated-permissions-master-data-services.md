---
title: Consolidado de permisos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], consolidated member attribute permissions
- consolidated members [Master Data Services], attribute permissions
- permissions [Master Data Services], consolidated members
- members [Master Data Services], consolidated member permissions
ms.assetid: 084055a3-5fd3-43f3-b620-ac6afab42a3d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 91c00dc638369d46986ee3757a6d889ed5a1439f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042906"
---
# <a name="consolidated-permissions-master-data-services"></a>Permisos consolidados (Master Data Services)
  Los permisos consolidados se aplican a los valores de atributo de todos los miembros consolidados de una entidad.  
  
 Los permisos consolidados solo se aplican a las entidades que estén habilitadas para jerarquías explícitas y colecciones.  
  
 **Notas:**  
  
-   Los permisos de hoja solo se aplican al área funcional del **Explorador** de la interfaz de usuario.  
  
-   Los permisos asignados a **Nombre** y a los atributos de **Código** no se aplican.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Solo lectura**|Se muestran los miembros consolidados, pero el usuario no los puede agregar, quitar o cambiar.|  
|**Update**|Se muestran los miembros consolidados y el usuario los puede agregar, quitar y cambiar.|  
|**Denegar**|No se muestran los miembros consolidados para la entidad.|  
  
## <a name="attribute-permissions"></a>Permisos de atributo  
 Los permisos de atributo se aplican a los valores del atributo para la entidad concreta. Los usuarios con permisos de atributo solo no se pueden agregar o quitar a miembros.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Solo lectura**|Se muestra el atributo, pero el usuario no puede cambiar los valores de atributo.|  
|**Update**|Se muestra el atributo y el usuario puede cambiar los valores de atributo.|  
|**Denegar**|No se muestra el atributo.<br /><br /> Nota: No puede denegar explícitamente el acceso a los atributos Code y Name.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [Permisos de hoja &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [Permisos de objeto del modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Miembros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
