---
title: "Miembros (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "miembros hoja [Master Data Services]"
  - "miembros consolidados [Master Data Services]"
  - "miembros consolidados [Master Data Services], acerca de los miembros consolidados"
  - "miembros [Master Data Services], acerca de los miembros"
  - "miembros hoja [Master Data Services], acerca de los miembros hoja"
  - "miembros [Master Data Services]"
ms.assetid: 0fda32b9-677d-4ba2-bb28-f76f2383a30f
caps.latest.revision: 16
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# Miembros (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los miembros son los datos maestros físicos. Por ejemplo, un miembro puede ser una bicicleta Road-150 de una entidad Product o un cliente específico de una entidad Customer.  
  
## Cómo se relacionan los miembros con otros objetos del modelo  
 Se puede considerar que los miembros son como filas de una tabla. Los miembros relacionados están contenidos en una entidad y cada miembro se define mediante valores de atributo.  
  
 En este ejemplo, la tabla representa una entidad, las filas serían los miembros y las columnas, los atributos. Cada celda representa un valor de atributo de un miembro concreto.  
  
 ![Entidad de Master Data Services representada como una tabla](../master-data-services/media/mds-conc-entity-table.gif "Entidad de Master Data Services representada como una tabla")  
  
## Tipos de miembro  
 Existen tres tipos de miembros: hoja, consolidados y de colección.  
  
 Los miembros hoja son los miembros predeterminados en una entidad.  
  
-   En las jerarquías derivadas, los miembros hoja son el único tipo de miembro. Los miembros hoja de una entidad se usan como elementos primarios de los miembros hoja de otra entidad.  
  
-   En las jerarquías explícitas, los miembros hoja son el nivel más bajo y no pueden tener elementos secundarios.  
  
 Los miembros consolidados solo existen cuando se habilitan jerarquías explícitas y colecciones para la entidad.  
  
-   Las jerarquías derivadas no contienen miembros consolidados.  
  
-   En las jerarquías explícitas, los miembros consolidados pueden ser elementos primarios de otros miembros de la jerarquía o pueden ser elementos secundarios.  
  
## Usar jerarquías y colecciones para organizar los miembros  
 Las jerarquías y las colecciones se pueden usar para agrupar miembros con fines de informes o análisis. Para obtener más información, consulte [Jerarquías &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md) y [Colecciones &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md).  
  
## Ejemplo de miembro  
 En el ejemplo siguiente, cada miembro se compone de los valores de atributo Name, Code, Subcategory, StandardCost, ListPrice y FilePhoto.  
  
 ![Tabla de entidades de producto de bicicleta](../master-data-services/media/mds-conc-entity-table-w-data.gif "Tabla de entidades de producto de bicicleta")  
  
## Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear un nuevo miembro hoja.|[Crear un miembro hoja &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Crear un nuevo miembro consolidado.|[Crear un miembro consolidado &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)|  
|Eliminar un miembro o colección existente.|[Eliminar un miembro o una colección &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)|  
|Reactivar un miembro o una colección eliminados.|[Reactivar un miembro o una colección &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)|  
|Actualizar los valores de atributo de un miembro.|[Cambar el tipo de atributo &#40;complemento MDS para Excel&#41;](../master-data-services/microsoft-excel-add-in/change-the-attribute-type-mds-add-in-for-excel.md)|  
|Mover miembros dentro de una jerarquía.|[Mover miembros dentro de una jerarquía &#40;Master Data Services&#41;](../Topic/Move%20Members%20within%20a%20Hierarchy%20\(Master%20Data%20Services\).md)|  
|Solucionar conflictos de combinación.|[Conflictos de combinación &#40;Master Data Services&#41;](../master-data-services/merge-conflicts-master-data-services.md)|  
  
## Contenido relacionado  
  
-   [Introducción a Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
-   [Jerarquías &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md)  
  
-   [Colecciones &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [Permisos de hoja &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)  
  
-   [Permisos consolidados &#40;Master Data Services&#41;](../Topic/Consolidated%20Permissions%20\(Master%20Data%20Services\).md)  
  
-   [Operadores de filtro &#40;Master Data Services&#41;](../master-data-services/filter-operators-master-data-services.md)  
  
  