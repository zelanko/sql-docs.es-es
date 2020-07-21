---
title: Permisos consolidados (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], consolidated member attribute permissions
- consolidated members [Master Data Services], attribute permissions
- permissions [Master Data Services], consolidated members
- members [Master Data Services], consolidated member permissions
ms.assetid: 084055a3-5fd3-43f3-b620-ac6afab42a3d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b40598eaa81ce0a1d890ef8ec37a12fada0fa458
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971905"
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
|**Deny**|No se muestran los miembros consolidados para la entidad.|  
  
## <a name="attribute-permissions"></a>Permisos de atributo  
 Los permisos de atributo se aplican a los valores del atributo para la entidad concreta. Los usuarios que solo tienen permisos de atributo no pueden agregar o quitar miembros.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Solo lectura**|Se muestra el atributo, pero el usuario no puede cambiar los valores de atributo.|  
|**Update**|Se muestra el atributo y el usuario puede cambiar los valores de atributo.|  
|**Deny**|No se muestra el atributo.<br /><br /> Nota: No puede denegar explícitamente el acceso a los atributos Name y Code.|  
  
## <a name="see-also"></a>Consulte también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [Permisos de hoja &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [Permisos del objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Miembros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
