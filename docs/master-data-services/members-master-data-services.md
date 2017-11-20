---
title: Miembros (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- leaf members [Master Data Services]
- consolidated members [Master Data Services]
- consolidated members [Master Data Services], about consolidated members
- members [Master Data Services], about members
- leaf members [Master Data Services], about leaf members
- members [Master Data Services]
ms.assetid: 0fda32b9-677d-4ba2-bb28-f76f2383a30f
caps.latest.revision: 16
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 3161b24f55c5473829b5d0a0ea090763d1203295
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="members-master-data-services"></a>Miembros (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los miembros son los datos maestros físicos. Por ejemplo, un miembro puede ser una bicicleta Road-150 de una entidad Product o un cliente específico de una entidad Customer.  
  
## <a name="how-members-relate-to-other-model-objects"></a>Cómo se relacionan los miembros con otros objetos del modelo  
 Se puede considerar que los miembros son como filas de una tabla. Los miembros relacionados están contenidos en una entidad y cada miembro se define mediante valores de atributo.  
  
 En este ejemplo, la tabla representa una entidad, las filas serían los miembros y las columnas, los atributos. Cada celda representa un valor de atributo de un miembro concreto.  
  
 ![Entidad de Master Data Services representada como una tabla](../master-data-services/media/mds-conc-entity-table.gif "Entidad de Master Data Services representada como una tabla")  
  
## <a name="member-types"></a>Tipos de miembro  
 Existen tres tipos de miembros: hoja, consolidados y de colección.  
  
 Los miembros hoja son los miembros predeterminados en una entidad.  
  
-   En las jerarquías derivadas, los miembros hoja son el único tipo de miembro. Los miembros hoja de una entidad se usan como elementos primarios de los miembros hoja de otra entidad.  
  
-   En las jerarquías explícitas, los miembros hoja son el nivel más bajo y no pueden tener elementos secundarios.  
  
 Los miembros consolidados solo existen cuando se habilitan jerarquías explícitas y colecciones para la entidad.  
  
-   Las jerarquías derivadas no contienen miembros consolidados.  
  
-   En las jerarquías explícitas, los miembros consolidados pueden ser elementos primarios de otros miembros de la jerarquía o pueden ser elementos secundarios.  
  
## <a name="use-hierarchies-and-collections-to-organize-members"></a>Usar jerarquías y colecciones para organizar los miembros  
 Las jerarquías y las colecciones se pueden usar para agrupar miembros con fines de informes o análisis. Para obtener más información, consulte [Jerarquías &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md) y [Colecciones &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md).  
  
## <a name="member-example"></a>Ejemplo de miembro  
 En el ejemplo siguiente, cada miembro se compone de los valores de atributo Name, Code, Subcategory, StandardCost, ListPrice y FilePhoto.  
  
 ![Tabla de entidades de producto de bicicleta](../master-data-services/media/mds-conc-entity-table-w-data.gif "Tabla de entidades de producto de bicicleta")  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear un nuevo miembro hoja.|[Crear un miembro hoja &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Crear un nuevo miembro consolidado.|[Crear un miembro consolidado &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)|  
|Eliminar un miembro o colección existente.|[Eliminar un miembro o una colección &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)|  
|Reactivar un miembro o una colección eliminados.|[Reactivar un miembro o una colección &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)|  
|Actualizar los valores de atributo de un miembro.|[Cambar el tipo de atributo &#40;complemento MDS para Excel&#41;](../master-data-services/microsoft-excel-add-in/change-the-attribute-type-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Introducción a Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
-   [Jerarquías &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md)  
  
-   [Colecciones &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [Permisos de hoja &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)  
  
 
-   [Operadores de filtro &#40;Master Data Services&#41;](../master-data-services/filter-operators-master-data-services.md)  
  
  

