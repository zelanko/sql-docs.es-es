---
title: Las medidas y grupos de medida | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 04eb5a41bec6e9abb62cfde516f2dad2ff820521
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024252"
---
# <a name="measures-and-measure-groups"></a>Medidas y grupos de medida
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un cubo incluye *medidas* en *grupos de medida*, lógica de negocios y una colección de dimensiones que proporcionan contexto para evaluar los datos numéricos que proporciona una medida. Las medidas y los grupos de medida son componentes esenciales de un cubo. Un cubo no puede existir sin, al menos, uno de cada uno de estos componentes.  
  
 En este tema se describen [Measures](#bkmk_measure) y [Measure Groups](#bkmk_mg). También contiene la siguiente tabla, con vínculos a procedimientos para crear y configurar grupos de medida y medidas.  
  
|**Vínculo**|**Description**|  
|--------------|---------------------|  
|[Crear medidas y grupos de medida en modelos multidimensionales](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|Elija uno de varios enfoques para crear medidas y grupos de medida.|  
|[Configurar propiedades de medidas](../../analysis-services/multidimensional-models/configure-measure-properties.md)|Si usa el Asistente para cubos para iniciar el cubo, puede que deba cambiar el método de agregación, aplicar un formato de datos, establecer la visibilidad de la medida en las aplicaciones cliente o, posiblemente, agregar una expresión de medida para manipular los datos antes de que se agreguen los valores.|  
|[Configurar las propiedades de grupo de medida](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)|En un modelo multidimensional, un grupo de medida equivale a una tabla de hechos en el almacén de datos de origen. Las propiedades de un grupo de medida le permiten especificar comportamientos de almacenamiento en caché, el almacenamiento y las directivas de procesamiento que funcionan en conjunto en el nivel del grupo de medida. La configuración de particiones está determinada en parte por las propiedades establecidas en los objetos de grupos de medida.|  
|[Usar funciones de agregado](../../analysis-services/multidimensional-models/use-aggregate-functions.md)|Asegúrese de comprender los métodos de agregación que se pueden asignar a una medida.|  
|[Definir el comportamiento de suma parcial](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)|El comportamiento de suma parcial corresponde a las agregaciones que son válidas para algunas dimensiones, pero no para otras. Un ejemplo común es un saldo de cuenta bancaria. Quizás quiera agregar saldos por cliente y región, pero no por tiempo. Por ejemplo, es poco probable que quiera agregar saldos de la misma cuenta en días consecutivos. Para definir el comportamiento de suma parcial, use el Asistente para agregar inteligencia empresarial.|  
|[Grupos de medida vinculados](../../analysis-services/multidimensional-models/linked-measure-groups.md)|Reasigne un grupo de medida existente de otros cubos a la misma base de datos o a diferentes bases de datos de Analysis Services.|  
  
##  <a name="bkmk_measure"></a> Measures  
 Una medida representa una columna que contiene datos cuantificables, normalmente numéricos, que se pueden agregar. Las medidas representan algunos aspectos de la actividad de la organización, expresada en términos económicos (como ingresos, márgenes o costos), como cuentas (niveles de inventario, cantidad de empleados, clientes o pedidos) o como un cálculo más complejo que incorpora la lógica de negocios.  
  
 Cada cubo debe tener al menos una medida, pero la mayoría tienen muchas, a veces, cientos. Estructuralmente, una medida se asigna, por lo general, a una columna de origen de una tabla de hechos. Dicha columna proporciona los valores usados para cargar la medida. De forma alternativa, también puede definir una medida mediante MDX.  
  
 Las medidas son contextuales, lo cual significa que funcionan con datos numéricos en un contexto que viene determinado por los miembros de dimensión que estén incluidos en la consulta. Por ejemplo, una medida que calcula **Reseller Sales** (las ventas del distribuidor) deberá estar respaldada por un operador **Sum** y agregará los importes de ventas para cada miembro de dimensión incluido en la consulta. Si la consulta especifica productos individuales, se acumula en una categoría o se segmenta por hora o ubicación geográfica, la medida debe producir una operación que sea válida para las dimensiones incluidas en la consulta.  
  
 En este ejemplo, **Reseller Sales** se agrega a varios niveles de la jerarquía **Sales Territory** (zona de ventas).  
  
 ![Tabla dinámica con medidas y dimensiones mencionadas](../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "tabla dinámica con medidas y dimensiones que se menciona dónde se encuentra")  
  
 Las medidas generan resultados válidos cuando la tabla de hechos que contiene los datos de origen numéricos también contiene punteros a las tablas de dimensiones que se usan en la consulta. En el ejemplo de Reseller Sales, si cada fila que contiene un importe de ventas también incluye un puntero a una tabla de productos, una tabla de fechas o una tabla de zona de ventas, las consultas que incluyan miembros de esas dimensiones se resolverán correctamente.  
  
 ¿Qué ocurre si la medida está relacionada con las dimensiones que se usan en la consulta? Normalmente, Analysis Services muestra la medida predeterminada, y el valor es el mismo para todos los miembros. En este ejemplo, **Internet Sales**(ventas por Internet), que mide las ventas directas a los clientes que usan el catálogo en línea, no tiene relación con la organización de ventas.  
  
 ![Valores de la medida de tabla dinámica que muestra repetidas](../../analysis-services/multidimensional-models/media/ssas-unrelatedmeasure.PNG "valores de medida de la tabla dinámica que muestra repetidos")  
  
 Para reducir las posibilidades de que se produzcan estos comportamientos en una aplicación cliente, puede crear varios cubos o perspectivas en la misma base de datos y asegurarse de que cada cubo o perspectiva contenga solo los objetos relacionados. Las relaciones que debe comprobar son las del grupo de medida (asignado a la tabla de hechos) con las dimensiones.  
  
##  <a name="bkmk_mg"></a> Measure Groups  
 En un cubo, las tablas de hechos subyacentes agrupan las medidas en grupos de medida. Los grupos de medida se utilizan para asociar dimensiones a medidas. Los grupos de medida también se utilizan para las medidas que tienen recuento distintivo como comportamiento de agregación. Si se coloca cada medida de recuento distintiva en su propio grupo de medida se optimiza el procesamiento de la agregación.  
  
 Un objeto <xref:Microsoft.AnalysisServices.MeasureGroup> simple se compone de información básica, como el nombre de grupo, el modo de almacenamiento y el modo de procesamiento. También contiene sus partes constitutivas: las medidas, las dimensiones y las particiones que componen el grupo de medida.  
  
## <a name="see-also"></a>Vea también  
 [Cubos en modelos multidimensionales](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [Crear medidas y grupos de medida en modelos multidimensionales](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)  
  
  
