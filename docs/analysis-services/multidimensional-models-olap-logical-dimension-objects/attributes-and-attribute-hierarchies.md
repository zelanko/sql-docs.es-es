---
title: "Atributos y jerarquías de atributo | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- regular attributes [Analysis Services]
- parent attributes [Analysis Services]
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], about attributes
- account attributes [Analysis Services]
- dimensions [Analysis Services], attributes
- key attributes [Analysis Services]
- OLAP objects [Analysis Services], attributes
- attributes [Analysis Services], relationships
- attributes [Analysis Services]
- relationships [Analysis Services], attributes
ms.assetid: 59de1ea2-e7a9-4a53-9ee0-14be52e95643
caps.latest.revision: "49"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: a86eb2f15fe0109a2e5b2492a61ca7102e662e7e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="attributes-and-attribute-hierarchies"></a>Atributos y jerarquías de atributos
  Las dimensiones son colecciones de atributos que están enlazados a una o varias columnas de una tabla o vista de la vista del origen de datos.  
  
## <a name="key-attribute"></a>Atributo clave  
 Cada dimensión contiene un atributo clave. Cada atributo está enlazado a una o varias columnas de una tabla de dimensiones. El atributo clave es el atributo de una dimensión que identifica las columnas de la tabla principal de dimensiones que se utilizan en las relaciones de clave externa con la tabla de hechos. Normalmente, el atributo clave representa a la columna o columnas de clave principal de la tabla de dimensiones. Puede definir una clave principal lógica en una tabla de una vista del origen de datos que carece de clave principal física en el origen de datos subyacente. **Para obtener más información**, consulte [definir claves principales lógicas en una vista del origen de datos &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md). Al definir atributos clave, el Asistente para cubos y el Asistente para dimensiones intentan hacer uso de las columnas de clave principal de la tabla de dimensiones en la vista del origen de datos. Si la tabla de dimensiones no tiene definida una clave principal lógica o una clave principal física, los asistentes no podrán definir correctamente los atributos clave de la dimensión.  
  
## <a name="binding-an-attribute-to-columns-in-data-source-view-tables-or-views"></a>Enlazar un atributo a columnas de tablas o vistas de vistas del origen de datos  
 Un atributo está enlazado a columnas de las tablas o vistas de una o varias vistas del origen de datos. Un atributo siempre está enlazado a una o más columnas de clave, lo que determina los miembros incluidos en el atributo. De manera predeterminada, es la única columna a la que está enlazado un atributo. Un atributo también se puede enlazar a una o más columnas adicionales para fines específicos. Por ejemplo, de un atributo **NameColumn** propiedad determina el nombre que aparece para el usuario para cada miembro de atributo: esta propiedad del atributo se puede enlazar a una columna de dimensión en particular a través de una vista del origen de datos o puede ser enlazar a una columna calculada en la vista del origen de datos. Para obtener más información, consulte [Dimension Attribute Properties Reference](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
## <a name="attribute-hierarchies"></a>Jerarquías de atributo  
 De forma predeterminada, los miembros de los atributos se organizan en jerarquías de dos niveles compuestas de un nivel hoja y un nivel Todos. El nivel Todos contiene el valor agregado de los miembros del atributo en las medidas de cada grupo de medida del que es miembro la dimensión con la que está relacionado el atributo. Sin embargo, si la **IsAggregatable** propiedad está establecida en False, no se crea el nivel todos. Para obtener más información, consulte [Dimension Attribute Properties Reference](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
 Los atributos pueden estar, y suelen estar, organizados en jerarquías definidas por el usuario que proporcionan las rutas de acceso de obtención de detalles mediante las cuales los usuarios pueden examinar los datos de los grupos de medida con los que está relacionado el atributo. En las aplicaciones cliente, los atributos se pueden utilizar para proporcionar información sobre agrupamientos y restricciones. Cuando los atributos se organizan en jerarquías definidas por el usuario, definir relaciones entre los niveles de jerarquía relación de varios a uno o una relación uno a uno (denominada una *natural* relación). Por ejemplo, en una jerarquía Calendar Time, el nivel Day se debe relacionar con el nivel Month, éste con el nivel Quarter y así sucesivamente. La definición de las relaciones entre los niveles de una jerarquía definida por el usuario permite que Analysis Services defina agregaciones más útiles para aumentar el rendimiento de las consultas; además, puede reducir el uso de memoria durante el procesamiento, algo que puede ser importante con cubos grandes o complejos. Para obtener más información, consulte [jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md), [Create User-Defined jerarquías](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md), y [definir relaciones de atributo](../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
## <a name="attribute-relationships-star-schemas-and-snowflake-schemas"></a>Relaciones de atributo, esquemas en estrella y esquemas de copo de nieve  
 De forma predeterminada, en un esquema en estrella, todos los atributos se relacionan directamente con el atributo clave, lo que permite a los usuarios examinar los hechos del cubo basándose en cualquier jerarquía de atributo de la dimensión. En un esquema de copo de nieve, un atributo está directamente vinculado al atributo clave si la tabla subyacente está directamente vinculada a la tabla de hechos o indirectamente vinculado por medio del atributo enlazado a la clave de la tabla subyacente que vincula la tabla de copo de nieve a la tabla vinculada directamente.  
  
## <a name="see-also"></a>Vea también  
 [Crear jerarquías definidas por el usuario](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [Definir relaciones de atributo](../../analysis-services/multidimensional-models/attribute-relationships-define.md)   
 [Referencia de las propiedades de los atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
