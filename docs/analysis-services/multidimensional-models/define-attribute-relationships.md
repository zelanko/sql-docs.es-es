---
title: "Definir relaciones de atributo | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "atributos [Analysis Services], relaciones"
  - "relaciones [Analysis Services], atributos"
ms.assetid: 9184d344-e96d-4025-ad6f-3f75129746df
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Definir relaciones de atributo
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], los atributos son la unidad de creación fundamental de una dimensión. Una dimensión contiene un conjunto de atributos que se organizan en función de las relaciones de atributo.  
  
 Para cada tabla incluida en una dimensión, hay una relación de atributo que relaciona el atributo clave de la tabla con otros atributos en esa tabla. Esta relación la crea al crear la dimensión.  
  
 Una relación de atributo proporciona las siguientes ventajas:  
  
-   Reduce la cantidad de memoria necesaria para procesar la dimensión. Esto acelera el procesamiento de dimensiones, particiones y consultas.  
  
-   Aumenta el rendimiento de las consultas porque el acceso al almacenamiento es más rápido y se optimizan mejor los planes de ejecución.  
  
-   Hace que los algoritmos de diseños de agregaciones seleccionen agregados más efectivos, siempre y cuando las jerarquías definidas por el usuario se hayan establecido a lo largo de las rutas de acceso de la relación.  
  
    > [!NOTE]  
    >  Para obtener más información sobre la importancia y las implicaciones de definir y configurar las relaciones de atributo, vea la sección “Enhancing query performance” (Mejora del rendimiento de las consultas) en [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621) (Guía de rendimiento de SQL Server 2005 Analysis Services).  
  
## Consideraciones sobre las relaciones de atributo  
 Si los datos subyacentes lo permiten, también debería definir relaciones de atributo únicas entre atributos. Para definir relaciones de atributo únicas, utilice la pestaña **Relación de los atributos** del Diseñador de dimensiones.  
  
 Cualquier atributo que tenga una relación de salida debe tener una clave única relativa a su atributo relacionado. En otras palabras, un miembro de un atributo de origen solo debe identificar un único miembro de un atributo relacionado. Por ejemplo, considere la relación, Ciudad -> Estado. En esta relación, el atributo de origen es Ciudad y el atributo relacionado es Estado. El atributo de origen es el lado "varios" y la parte relacionada es el lado "uno" de la relación de varios a uno. La clave para el atributo de origen sería Ciudad + Estado. Para obtener más información, vea [Crear, modificar o eliminar una relación de atributo](../../analysis-services/multidimensional-models/create-modify-or-delete-an-attribute-relationship.md).  
  
 Para obtener más información sobre las propiedades de una relación de atributo, vea [Configurar propiedades de relación de los atributos](../../analysis-services/multidimensional-models/configure-attribute-relationship-properties.md).  
  
> [!NOTE]  
>  Si las relaciones de atributo no se definen correctamente, puede que los resultados de las consultas no sean válidos.  
  
## Vea también  
 [Relaciones de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  