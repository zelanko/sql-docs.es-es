---
title: Introducción a las dimensiones (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], about dimensions
- storage [Analysis Services], dimensions
- dimensions [Analysis Services], examples
- storing data [Analysis Services], dimensions
- storage [Analysis Services]
ms.assetid: ab170fdd-4144-42db-9497-690b9189fc25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d60d86a333c38b1fe122d72f55ccba25653256c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702520"
---
# <a name="introduction-to-dimensions-analysis-services---multidimensional-data"></a>Introducción a las dimensiones (Analysis Services - Datos multidimensionales)
  Todos los Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dimensiones son grupos de atributos basados en columnas de tablas o vistas en una vista del origen de datos. Las dimensiones son independientes de un cubo, se pueden utilizar en varios cubos, se pueden emplear varias veces en un único cubo y pueden vincularse entre instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Una dimensión independiente de un cubo se denomina dimensión de base de datos, mientras que una instancia de una dimensión de base de datos de un cubo se denomina dimensión de cubo.  
  
## <a name="dimension-based-on-a-star-schema-design"></a>Dimensión basada en un diseño de esquema en estrella  
 La estructura de una dimensión depende en gran medida de la estructura de la tabla o tablas de dimensiones subyacentes. La estructura más sencilla se denomina esquema en estrella, en la que cada dimensión se basa en una única tabla de dimensiones que se vincula directamente a la tabla de hechos mediante una relación de clave principal a clave externa.  
  
 El siguiente diagrama muestra una subsección de la [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] base de datos de ejemplo, en el que el **FactResellerSales** relacionados con la tabla de hechos para dos tablas de dimensiones, **DimReseller** y **DimPromotion**. El **ResellerKey** columna en el **FactResellerSales** tabla de hechos define una relación de clave externa a la **ResellerKey** columna de clave principal en el  **DimReseller** tabla de dimensiones. De forma similar, el **PromotionKey** columna en el **FactResellerSales** tabla de hechos define una relación de clave externa a la **PromotionKey** columna de clave principal en el  **DimPromotion** tabla de dimensiones.  
  
 ![Esquema lógico de relación de dimensión de hechos](../../../2014/analysis-services/dev-guide/media/dimfactrelationship.gif "esquema lógico de relación de dimensión de hechos")  
  
## <a name="dimension-based-on-a-snowflake-schema-design"></a>Dimensión basada en un diseño de esquema de copo de nieve  
 Normalmente se necesita una estructura más compleja, dado que se necesita la información de varias tablas para definir la dimensión. En esta estructura, denominada esquema de copo de nieve, cada dimensión se basa en los atributos de las columnas de varias tablas vinculadas entre sí y a la tabla de hechos mediante relaciones de clave principal a clave externa. Por ejemplo, el siguiente diagrama muestra las tablas necesarias para describir por completo la dimensión Product en el **AdventureWorksDW** proyecto de ejemplo:  
  
 ![Las tablas de dimensión de producto de AdventureWorksAS](../../../2014/analysis-services/dev-guide/media/dimproduct.gif "tablas de dimensión de producto de AdventureWorksAS")  
  
 Para describir completamente un producto, la categoría y la subcategoría del producto deben incluirse en la dimensión de producto. Sin embargo, esa información no reside directamente en la tabla principal para el **DimProduct** dimensión. Una relación de clave externa de **DimProduct** a **DimProductSubcategory**, que a su vez tiene una relación de clave externa a la **DimProductCategory** de tabla, facilita el es posible que incluya la información de categorías de productos y las subcategorías de la dimensión Product.  
  
## <a name="snowflake-schema-versus-reference-relationship"></a>Esquema de copo de nieve frente a relación de referencia  
 Algunas veces se puede optar entre utilizar un esquema en estrella para definir los atributos de una dimensión a partir de varias tablas, o bien definir dos dimensiones independientes y una relación de dimensión de referencia entre ellas. En el siguiente diagrama se muestra este tipo de escenario.  
  
 ![Esquema lógico de la dimensión de ejemplo que se hace referencia](../../../2014/analysis-services/dev-guide/media/dimindirect.gif "esquema lógico de la dimensión de ejemplo que se hace referencia")  
  
 En el diagrama anterior, el **FactResellerSales** tabla de hechos no tiene una relación de clave externa con la **DimGeography** tabla de dimensiones. Sin embargo, el **FactResellerSales** tabla de hechos tienen una relación de clave externa con la **DimReseller** tabla de dimensiones, que a su vez tiene una relación de clave externa con la  **DimGeography** tabla de dimensiones. Para definir una dimensión Reseller que contenga información geográfica acerca de cada distribuidor, tendrá que recuperar estos atributos desde la **DimGeography** y **DimReseller** tablas de dimensiones. Sin embargo, en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], se puede obtener el mismo resultado si se crean dos dimensiones independientes y se vinculan a un grupo de medida definiendo una relación de dimensión de referencia entre las dos dimensiones. Para obtener más información acerca de las relaciones de dimensión de referencia, consulte [relaciones de dimensión](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 Una ventaja del uso de relaciones de dimensiones de referencia en este escenario es que es posible crear una única dimensión geográfica y, a continuación, crear varias dimensiones de cubo basadas en la dimensión geográfica, sin que se necesite espacio de almacenamiento adicional. Por ejemplo, puede vincular una de las dimensiones de cubo geográficas a una dimensión de distribuidor y otra de las dimensiones de cubo geográficas a una dimensión de cliente. **Temas relacionados:**[relaciones de dimensión](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md), [definir relaciones referenciadas y propiedades de la relación hace referencia](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
## <a name="processing-a-dimension"></a>Procesar una dimensión  
 Tras crear una dimensión, debe procesarla antes de poder ver los miembros de sus atributos y sus jerarquías. Tras modificar la estructura de una dimensión o actualizar la información de sus tablas subyacentes, tiene que volver a procesar la dimensión antes de poder ver los cambios. Cuando se procesa una dimensión después de realizar cambios estructurales, se deben procesar también los cubos que incluyen la dimensión, ya que de lo contrario el cubo no se podrá ver.  
  
## <a name="security"></a>Seguridad  
 La seguridad de todos los objetos subordinados de una dimensión, incluidos las jerarquías, niveles y miembros, se establece utilizando roles en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La seguridad de las dimensiones se puede aplicar a todos los cubos de la base de datos que utilizan la dimensión o solo a determinado cubo. Para obtener más información acerca de la seguridad de dimensión, vea [conceder permisos en una dimensión &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de dimensiones](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [Traducciones de dimensiones](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Dimensiones habilitadas para escritura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
