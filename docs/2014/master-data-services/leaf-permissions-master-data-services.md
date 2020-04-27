---
title: Permisos de hoja (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], permissions
- members [Master Data Services], leaf member permissions
- permissions [Master Data Services], leaf members
- leaf members [Master Data Services], attribute permissions
- attributes [Master Data Services], leaf member attribute permissions
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ee587881b95821c2ae23580b54d298fa496cec15
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479170"
---
# <a name="leaf-permissions-master-data-services"></a>Permisos de hoja (Master Data Services)
  Los permisos de hoja se aplican a los valores de atributo de todos los miembros hoja de una entidad.  
  
 Para las entidades sin jerarquías explícitas habilitadas, la asignación de un permiso a **Hoja** es equivalente a asignar un permiso a la entidad.  
  
 **Notas:**  
  
-   Los permisos de hoja solo se aplican al área funcional del **Explorador** de la interfaz de usuario.  
  
-   Los permisos asignados a **Nombre** y a los atributos de **Código** no se aplican.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Solo lectura**|Se muestran los miembros hoja, pero el usuario no los puede agregar, quitar o cambiar.<br /><br /> Si hay miembros consolidados, se muestran los nombres y códigos pero el usuario no los puede agregar, quitar o cambiar.|  
|**Actualizar**|Se muestran los miembros hoja y el usuario los puede agregar, quitar y cambiar.<br /><br /> Si hay miembros consolidados, se muestran los nombres y códigos pero el usuario no los puede agregar, quitar o cambiar.|  
|**Deny**|No se muestran los miembros hoja para la entidad.|  
  
## <a name="attribute-permissions"></a>Permisos de atributo  
 Los permisos de atributo se aplican a los valores del atributo para la entidad concreta. Los usuarios que tengan únicamente permisos de atributo no pueden agregar o quitar miembros.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Solo lectura**|Se muestra el atributo, pero el usuario no puede cambiar los valores de atributo.|  
|**Actualizar**|Se muestra el atributo y el usuario puede cambiar los valores de atributo.|  
|**Deny**|No se muestra el atributo.<br /><br /> Nota: No puede denegar explícitamente el acceso a los atributos Name y Code.|  
  
### <a name="example"></a>Ejemplo  
 Para la entidad Product, asigne el permiso **Actualizar** al atributo Subcategory. Deniegue el permiso al resto de los atributos.  
  
|NOMBRE|Código|Subcategory (actualizar)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5}Bicicletas de montaña|  
|Mountain-100|BK-M201|{5}Bicicletas de montaña|  
  
 En el **Explorador**, puede actualizar cualquier valor de atributo en la columna Subcategory. Si no dispone del permiso para un atributo, este no se mostrará.  
  
> [!NOTE]  
>  En este ejemplo, Subcategory es un atributo basado en dominio, que depende de la entidad SubcategoryList. Puede seleccionar una subcategoría diferente para Mountain-100, pero no puede agregar o eliminar miembros en la entidad SubcategoryList.  
  
## <a name="see-also"></a>Consulte también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [Permisos consolidados &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)   
 [Permisos del objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Miembros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
