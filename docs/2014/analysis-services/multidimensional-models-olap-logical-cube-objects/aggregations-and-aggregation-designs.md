---
title: Agregaciones y diseños de agregaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- aggregations [Analysis Services], about aggregations
- storage [Analysis Services], aggregations
- Storage Design Wizard
- data summary [Analysis Services]
- data storage [Analysis Services]
- storing data [Analysis Services], aggregations
- aggregations [Analysis Services]
ms.assetid: 35bd8589-39fa-4e0b-b28f-5a07d70da0a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3897c5e41e16af0a8162b63794760aa4d740353d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727701"
---
# <a name="aggregations-and-aggregation-designs"></a>Agregaciones y diseños de agregaciones
  Un objeto <xref:Microsoft.AnalysisServices.AggregationDesign> define un conjunto de definiciones de agregación que se pueden compartir entre varias particiones.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Aggregation> representa el resumen de los datos de grupo de medida en una granularidad determinada de las dimensiones.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Aggregation> simple se compone de la información básica y dimensiones. La información Básica incluye el nombre de la agregación, el identificador, anotaciones y una descripción. Las dimensiones son una colección de objetos <xref:Microsoft.AnalysisServices.AggregationDimension> que contienen la lista de atributos de granularidad de la dimensión.  
  
 Las agregaciones son resúmenes de datos precalculados de las celdas hoja. Las agregaciones mejoran el tiempo de respuesta de las consultas al preparar las respuestas antes de que se formulen las preguntas. Por ejemplo, cuando una tabla de hechos de un almacenamiento de datos contiene cientos de miles de filas, puede tardar en responderse una consulta en la que se soliciten los totales de las ventas semanales de una determinada línea de productos si hay que recorrer y sumar todas las filas de la tabla de hechos para calcular la respuesta en el momento de la consulta. Sin embargo, la respuesta podría ser casi inmediata si se han precalculado los datos de resumen para responder a esta consulta. El precálculo de los datos de resumen se produce durante el procesamiento y constituye la base de los tiempos de respuesta rápida de la tecnología OLAP.  
  
 Los cubos son la forma en que la tecnología OLAP organiza los datos de resumen en estructuras multidimensionales. Las dimensiones y sus jerarquías de atributos reflejan las consultas que se pueden hacer al cubo. Las agregaciones se almacenan en la estructura multidimensional en celdas cuyas coordenadas especifican las dimensiones. Por ejemplo, la pregunta "¿Cuáles fueron las ventas del producto X en 1998 para la región Northwest?" implica tres dimensiones (producto, hora y geografía) y una medida (ventas). La respuesta es el valor de la celda del cubo que se encuentra en las coordenadas especificadas (producto X, 1998, Northwest); es decir, un valor numérico simple.  
  
 Otras preguntas pueden devolver varios valores. Por ejemplo: "¿Cuáles fueron las ventas de productos de hardware por trimestre y región en 1998?". Estas consultas devuelven conjuntos de celdas de las coordenadas que satisfacen las condiciones especificadas. El número de celdas devueltas por la consulta depende del número de elementos del nivel Hardware de la dimensión Product, los cuatro trimestres de 1998 y el número de regiones de la dimensión Geography. Si todos los datos de resumen se han precalculado en agregaciones, el tiempo de respuesta de la consulta solamente dependerá del tiempo que se necesite para extraer las celdas especificadas. No es necesario calcular ni leer datos de la tabla de hechos.  
  
 Aunque el precálculo de todas las posibles agregaciones de un cubo puede acelerar al máximo el tiempo de respuesta de todas las consultas, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede calcular con facilidad determinados valores agregados a partir de otras agregaciones precalculadas. Además, el cálculo de todas las agregaciones posibles requiere gran cantidad de tiempo de procesamiento y espacio de almacenamiento. Por lo tanto, existe un equilibrio entre los requisitos de almacenamiento y el porcentaje de posibles agregaciones que se precalculan. Si no se precalculan agregaciones (0%), la cantidad de tiempo de procesamiento y de espacio de almacenamiento que se necesita para un cubo se reduce al mínimo, aunque el tiempo de respuesta puede ser lento, ya que es preciso recuperar de las celdas hoja los datos necesarios para responder a cada consulta y luego agregarlos en el tiempo de la consulta para responder a cada una de ellas. Por ejemplo, para devolver un único número que responda a la pregunta planteada anteriormente ("¿Cuáles fueron las ventas del producto X en 1998 para la región noroeste?") sería necesario leer miles de filas de datos, extraer el valor de la columna utilizada para proporcionar la medida Sales de cada fila y, a continuación, calcular la suma. Además, el período de tiempo necesario para recuperar los datos dependerá en gran parte del modo de almacenamiento elegido para los datos: MOLAP, HOLAP o ROLAP.  
  
## <a name="designing-aggregations"></a>Diseñar agregaciones  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incorpora un algoritmo sofisticado para seleccionar agregaciones para el precálculo, de modo que se puedan calcular rápidamente otras agregaciones a partir de los valores precalculados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por ejemplo, si se han precalculado agregaciones para el nivel Month de una jerarquía Time, los cálculos de un nivel Quarter solamente necesitarán el resumen de tres números, operación que se puede realizar rápidamente a petición. Esta técnica ahorra tiempo de procesamiento y reduce los requisitos de almacenamiento, con el mínimo efecto en el tiempo de respuesta de consultas.  
  
 El Asistente para diseñar agregaciones permite especificar las restricciones de almacenamiento y porcentaje del algoritmo para conseguir un equilibrio satisfactorio entre el tiempo de respuesta de consultas y los requisitos de almacenamiento. Sin embargo, el algoritmo del Asistente para diseñar agregaciones asume que todas las posibles consultas son igualmente probables. El Asistente para optimización basada en el uso permite ajustar el diseño de la agregación de un grupo de medida mediante el análisis de las consultas enviadas por las aplicaciones cliente. Al utilizar el asistente para ajustar la agregación de un cubo, se puede mejorar el tiempo de respuesta de las consultas más frecuentes y reducir el tiempo de respuesta de aquellas consultas poco frecuentes sin afectar sustancialmente a las necesidades de almacenamiento del cubo.  
  
 Las agregaciones se diseñan con los asistentes, pero no se calculan hasta que se procesa la partición para la que se han diseñado. Una vez creada la agregación, si cambia la estructura de un cubo o se agregan o cambian datos de las tablas de origen de un cubo, suele ser necesario revisar las agregaciones del cubo y volver a procesarlo.  
  
## <a name="see-also"></a>Consulte también  
 [Procesamiento y modos de almacenamiento de particiones](partitions-partition-storage-modes-and-processing.md)  
  
  
