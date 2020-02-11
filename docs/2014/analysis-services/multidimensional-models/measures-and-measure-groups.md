---
title: Medidas y grupos de medida | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- measure groups [Analysis Services]
- measures [Analysis Services], about measures
- OLAP objects [Analysis Services], measures
- aggregate functions [Analysis Services]
- granularity
- measure groups [Analysis Services], about measure groups
- measures [Analysis Services]
- aggregations [Analysis Services], measures
- fact tables [Analysis Services]
ms.assetid: 4f0122f9-c3a5-4172-ada3-5bc5f7b1cc9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 63b035bd0ce315ccf1334c53e7ee1718c7569dac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073666"
---
# <a name="measures-and-measure-groups"></a>Medidas y grupos de medida
  Un cubo incluye *medidas* en *grupos de medida*, lógica de negocios y una colección de dimensiones que proporcionan contexto para evaluar los datos numéricos que proporciona una medida. Las medidas y los grupos de medida son componentes esenciales de un cubo. Un cubo no puede existir sin, al menos, uno de cada uno de estos componentes.  
  
 En este tema se describen [Measures](#bkmk_measure) y [Measure Groups](#bkmk_mg). También contiene la siguiente tabla, con vínculos a procedimientos para crear y configurar grupos de medida y medidas.  
  
|**Vínculo**|**Descripción**|  
|--------------|---------------------|  
|[Crear medidas y grupos de medida en modelos multidimensionales](create-measures-and-measure-groups-in-multidimensional-models.md)|Elija uno de varios enfoques para crear medidas y grupos de medida.|  
|[Configurar propiedades de medidas](configure-measure-properties.md)|Si usa el Asistente para cubos para iniciar el cubo, puede que deba cambiar el método de agregación, aplicar un formato de datos, establecer la visibilidad de la medida en las aplicaciones cliente o, posiblemente, agregar una expresión de medida para manipular los datos antes de que se agreguen los valores.|  
|[Configurar las propiedades de los grupos de medida](configure-measure-group-properties.md)|En un modelo multidimensional, un grupo de medida equivale a una tabla de hechos en el almacén de datos de origen. Las propiedades de un grupo de medida le permiten especificar comportamientos de almacenamiento en caché, el almacenamiento y las directivas de procesamiento que funcionan en conjunto en el nivel del grupo de medida. La configuración de particiones está determinada en parte por las propiedades establecidas en los objetos de grupos de medida.|  
|[Usar funciones de agregado](use-aggregate-functions.md)|Asegúrese de comprender los métodos de agregación que se pueden asignar a una medida.|  
|[Define Semiadditive Behavior](define-semiadditive-behavior.md)|El comportamiento de suma parcial corresponde a las agregaciones que son válidas para algunas dimensiones, pero no para otras. Un ejemplo común es un saldo de cuenta bancaria. Quizás quiera agregar saldos por cliente y región, pero no por tiempo. Por ejemplo, es poco probable que quiera agregar saldos de la misma cuenta en días consecutivos. Para definir el comportamiento de suma parcial, use el Asistente para agregar inteligencia empresarial.|  
|[Grupos de medida vinculados](linked-measure-groups.md)|Reasigne un grupo de medida existente de otros cubos a la misma base de datos o a diferentes bases de datos de Analysis Services.|  
  
##  <a name="bkmk_measure"></a>Cuantas  
 Una medida representa una columna que contiene datos cuantificables, normalmente numéricos, que se pueden agregar. Las medidas representan algunos aspectos de la actividad de la organización, expresada en términos económicos (como ingresos, márgenes o costos), como cuentas (niveles de inventario, cantidad de empleados, clientes o pedidos) o como un cálculo más complejo que incorpora la lógica de negocios.  
  
 Cada cubo debe tener al menos una medida, pero la mayoría tienen muchas, a veces, cientos. Estructuralmente, una medida se asigna, por lo general, a una columna de origen de una tabla de hechos. Dicha columna proporciona los valores usados para cargar la medida. De forma alternativa, también puede definir una medida mediante MDX.  
  
 Las medidas son contextuales, lo cual significa que funcionan con datos numéricos en un contexto que viene determinado por los miembros de dimensión que estén incluidos en la consulta. Por ejemplo, una medida que calcula las **ventas del distribuidor** estará respaldada por un `Sum` operador y agregará los importes de ventas de cada miembro de dimensión incluido en la consulta. Si la consulta especifica productos individuales, se acumula en una categoría o se segmenta por hora o ubicación geográfica, la medida debe producir una operación que sea válida para las dimensiones incluidas en la consulta.  
  
 En este ejemplo, **Reseller Sales** se agrega a varios niveles de la jerarquía **Sales Territory** (zona de ventas).  
  
 ![PivotTable con medidas y dimensiones indicadas](../media/ssas-keyconcepts-pivot1-measures-dimensions.png "PivotTable con medidas y dimensiones indicadas")  
  
 Las medidas generan resultados válidos cuando la tabla de hechos que contiene los datos de origen numéricos también contiene punteros a las tablas de dimensiones que se usan en la consulta. En el ejemplo de Reseller Sales, si cada fila que contiene un importe de ventas también incluye un puntero a una tabla de productos, una tabla de fechas o una tabla de zona de ventas, las consultas que incluyan miembros de esas dimensiones se resolverán correctamente.  
  
 ¿Qué ocurre si la medida está relacionada con las dimensiones que se usan en la consulta? Normalmente, Analysis Services muestra la medida predeterminada, y el valor es el mismo para todos los miembros. En este ejemplo, **Internet Sales**(ventas por Internet), que mide las ventas directas a los clientes que usan el catálogo en línea, no tiene relación con la organización de ventas.  
  
 ![Tabla dinámica que muestra valores de medida repetidos](../media/ssas-unrelatedmeasure.PNG "Tabla dinámica que muestra valores de medida repetidos")  
  
 Para reducir las posibilidades de que se produzcan estos comportamientos en una aplicación cliente, puede crear varios cubos o perspectivas en la misma base de datos y asegurarse de que cada cubo o perspectiva contenga solo los objetos relacionados. Las relaciones que debe comprobar son las del grupo de medida (asignado a la tabla de hechos) con las dimensiones.  
  
##  <a name="bkmk_mg"></a>Grupos de medida  
 En un cubo, las tablas de hechos subyacentes agrupan las medidas en grupos de medida. Los grupos de medida se utilizan para asociar dimensiones a medidas. Los grupos de medida también se utilizan para las medidas que tienen recuento distintivo como comportamiento de agregación. Si se coloca cada medida de recuento distintiva en su propio grupo de medida se optimiza el procesamiento de la agregación.  
  
 Un objeto <xref:Microsoft.AnalysisServices.MeasureGroup> simple se compone de información básica, como el nombre de grupo, el modo de almacenamiento y el modo de procesamiento. También contiene sus partes constitutivas: las medidas, las dimensiones y las particiones que componen el grupo de medida.  
  
## <a name="see-also"></a>Consulte también  
 [Cubos en modelos multidimensionales](cubes-in-multidimensional-models.md)   
 [Crear medidas y grupos de medida en modelos multidimensionales](create-measures-and-measure-groups-in-multidimensional-models.md)  
  
  
