---
title: Permisos de hoja (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attribute groups [Master Data Services], permissions
- members [Master Data Services], leaf member permissions
- permissions [Master Data Services], leaf members
- leaf members [Master Data Services], attribute permissions
- attributes [Master Data Services], leaf member attribute permissions
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93267daf8957c8c731d03ac03b647f9411c46396
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="leaf-permissions-master-data-services"></a>Permisos de hoja (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Los permisos de hoja se aplican a los valores de atributo de todos los miembros hoja de una entidad.  
  
 Para las entidades sin jerarquías explícitas habilitadas, la asignación de un permiso a **Hoja** es equivalente a asignar un permiso a la entidad.  
  
 **Notas:**  
  
-   Los permisos de hoja solo se aplican al área funcional del **Explorador** de la interfaz de usuario.  
  
-   Los permisos asignados a **Nombre** y a los atributos de **Código** no se aplican.  
  
|Permiso|Description|  
|----------------|-----------------|  
|**Lectura**|El usuario puede leer miembros hoja y atributos.|  
|**Crear**|Usuario puede crear miembros hoja y asignar valores de atributo durante la creación.|  
|**Update**|El usuario puede actualizar miembros hoja y atributos.|  
|**Eliminar**|El usuario puede eliminar miembros hoja.|  
|**Denegar**|Denegar todo el acceso a los miembros hoja.|  
  
 Los permisos de lectura, creación, actualización y eliminación se pueden combinar. Cuando se asignan Crear, Actualizar y Eliminar, el permiso de lectura se asigna automáticamente.  
  
## <a name="attribute-permissions"></a>Permisos de atributo  
 Los permisos de atributo se aplican a los valores del atributo para la entidad concreta. Los usuarios que tengan únicamente permisos de atributo no pueden agregar o quitar miembros.  
  
|Permiso|Description|  
|----------------|-----------------|  
|**Lectura**|El usuario puede leer atributos.|  
|**Crear**|El usuario puede asignar valores al crear miembros.|  
|**Update**|El usuario puede actualizar atributos.|  
|**Eliminar**|Ningún efecto.|  
|**Denegar**|No se muestra el atributo.<br /><br /> Nota: No puede denegar explícitamente el acceso a los atributos Name y Code.|  
  
### <a name="example"></a>Ejemplo  
 Para la entidad Product, asigne el permiso **Actualizar** al atributo Subcategory. Deniegue el permiso al resto de los atributos.  
  
|Nombre|código|Subcategory (actualizar)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5} Mountain Bikes|  
|Mountain-100|BK-M201|{5} Mountain Bikes|  
  
 En el **Explorador**, puede actualizar cualquier valor de atributo en la columna Subcategory. Si no dispone del permiso para un atributo, este no se mostrará.  
  
> [!NOTE]  
>  En este ejemplo, Subcategory es un atributo basado en dominio, que depende de la entidad SubcategoryList. Puede seleccionar una subcategoría diferente para Mountain-100, pero no puede agregar o eliminar miembros en la entidad SubcategoryList.  
  
## <a name="see-also"></a>Ver también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
    
 [Permisos de objeto del modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Miembros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
