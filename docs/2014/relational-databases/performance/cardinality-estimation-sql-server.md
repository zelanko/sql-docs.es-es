---
title: Estimación de cardinalidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.openlocfilehash: 5a81849f65e5b71acf233febb61e7725ec1e804e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107167"
---
# <a name="cardinality-estimation-sql-server"></a>Estimación de cardinalidad (SQL Server)
  La lógica de estimación de cardinalidad, denominada Estimador de cardinalidad, se ha rediseñado en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para mejorar la calidad de los planes de consulta y, por tanto, para mejorar el rendimiento de las consultas. El nuevo estimador de cardinalidad incorpora suposiciones y algoritmos que funcionan bien en las cargas de trabajo OLTP y de almacenamiento de datos modernas. Se basa en un profundo estudio sobre la estimación de cardinalidad en las cargas de trabajo modernas y en lo que hemos aprendido durante los últimos 15 años para mejorar el estimador de cardinalidad de SQL Server. Los comentarios de los clientes indican que si bien la mayoría de las consultas se beneficiarán del cambio o no cambiarán, un número reducido puede mostrar regresiones en comparación con el estimador de cardinalidad anterior.  
  
> [!NOTE]  
>  Las estimaciones de cardinalidad son una predicción del número de filas del resultado de la consulta. El optimizador de consultas utiliza estas estimaciones a la hora de elegir un plan para ejecutar la consulta. La calidad del plan de consulta tiene un impacto directo sobre la mejora del rendimiento de las consultas.  
  
## <a name="performance-testing-and-tuning-recommendations"></a>Recomendaciones sobre las pruebas y la optimización del rendimiento  
 El nuevo estimador de cardinalidad está habilitado para todas las bases de datos nuevas creadas en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Sin embargo, la actualización a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] no habilita el nuevo estimador de cardinalidad en las bases de datos existentes.  
  
 Para garantizar el máximo rendimiento de las consultas, siga estas recomendaciones para probar la carga de trabajo con el nuevo estimador de cardinalidad antes de habilitarlo en el sistema de producción.  
  
1.  Actualice todas las bases de datos existentes para que utilicen el nuevo estimador de cardinalidad. Para ello, use [nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) para establecer el nivel de compatibilidad de base de datos en 120.  
  
2.  Ejecute la carga de trabajo de prueba con el nuevo estimador de cardinalidad y solucione cualquier problema nuevo de rendimiento del mismo modo que lo hace ahora.  
  
3.  Una vez que se está ejecutando la carga de trabajo con el nuevo Estimador de cardinalidad (nivel de compatibilidad de base de datos (SQL Server 2014) 120) y ha hecho la regresión de una consulta concreta, puede ejecutar la consulta con la marca de seguimiento 9481 para usar la versión del estimador de cardinalidad utilizado en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]y versiones anteriores. Para ejecutar una consulta con una marca de seguimiento, vea el artículo de KB [Habilitar el plan afecta al comportamiento del optimizador de consultas de SQL Server, que se puede controlar mediante distintas marcas de seguimiento en un nivel de consulta específico](http://support.microsoft.com/kb/2801413).  
  
4.  Si no se puede cambiar todas las bases de datos a la vez para que utilicen el nuevo Estimador de cardinalidad, puede usar el Estimador de cardinalidad anterior para todas las bases de datos mediante [nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) a establecer el nivel de compatibilidad de base de datos a 110.  
  
5.  Si la carga de trabajo se está ejecutando con el nivel de compatibilidad de base de datos 110 y desea probar o ejecutar una consulta concreta con el nuevo estimador de cardinalidad, puede ejecutar la consulta con la marca de seguimiento 2312 para utilizar la versión de SQL Server 2014 del estimador de cardinalidad.  Para ejecutar una consulta con una marca de seguimiento, vea el artículo de KB [Habilitar el plan afecta al comportamiento del optimizador de consultas de SQL Server, que se puede controlar mediante distintas marcas de seguimiento en un nivel de consulta específico](http://support.microsoft.com/kb/2801413).  
  
## <a name="new-xevents"></a>Nuevos XEvents  
 Hay dos nuevos XEvents query_optimizer_estimate_cardinality para admitir los nuevos planes de consulta.  
  
-   *query_optimizer_estimate_cardinality* se produce cuando el optimizador de consultas calcula la cardinalidad de una expresión relacional.  
  
-   *query_optimizer_force_both_cardinality_estimation*_behaviors se produce cuando están habilitadas las marcas de seguimiento 2312 y 9481, intentando forzar el comportamiento anterior y nuevo de la estimación de cardinalidad al mismo tiempo.  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se muestran algunos cambios en las nuevas estimaciones de cardinalidad. Se ha vuelto a escribir el código para estimar la cardinalidad. La lógica es compleja y no es posible proporcionar una lista exhaustiva de todos los cambios.  
  
> [!NOTE]  
>  Estos ejemplos se proporcionan como información conceptual. No se requiere ninguna acción por su parte para cambiar la manera de diseñar las bases de datos y las consultas.  
  
### <a name="example-a-new-cardinality-estimates-use-an-average-cardinality-for-recently-added-ascending-data"></a>Ejemplo A. Las nuevas estimaciones de cardinalidad utilizan una cardinalidad promedio para los datos ascendentes recién agregados.  
 En este ejemplo se muestra cómo el nuevo estimador de cardinalidad puede mejorar las estimaciones de cardinalidad para los datos ascendentes que superan el valor máximo de la tabla durante la actualización de estadísticas más reciente.  
  
```  
SELECT item, category, amount FROM dbo.Sales AS s WHERE Date = '2013-12-19';  
```  
  
 En este ejemplo, se agregan nuevas filas a la tabla Sales cada día, la consulta solicita las ventas realizadas el 19/12/2013 y las estadísticas se actualizaron por última vez el 18/12/2013. El estimador de cardinalidad anterior supone que los valores de 19/12/2013 no existen porque la fecha supera la fecha máxima y las estadísticas no se han actualizado para incluir los valores de 19/12/2013. Esta situación, conocida como el problema de clave ascendente, se producirá si carga datos durante el día y ejecuta consultas en los datos antes de que se actualicen las estadísticas.  
  
 Este comportamiento ha cambiado. Ahora, incluso aunque no se hayan actualizado las estadísticas para los datos ascendentes más recientes que se agregan desde la última actualización de las estadísticas, el nuevo estimador de cardinalidad supone que existen los valores y utiliza la cardinalidad promedio para cada valor de la columna como la estimación de cardinalidad.  
  
### <a name="example-b-new-cardinality-estimates-assume-filtered-predicates-on-the-same-table-have-some-correlation"></a>Ejemplo B. Las nuevas estimaciones de cardinalidad suponen que los predicados filtrados en la misma tabla tienen alguna correlación.  
 En este ejemplo, suponga que la tabla Cars tiene 1000 filas, Make tiene 200 coincidencias de 'Honda', Model tiene 50 coincidencias de 'Civic' y que todos los Civics son Honda. Por tanto, el 20 % de los valores de la columna Make son 'Honda', el 5 % de los valores de la columna Model son 'Civic' y el número real de Honda Civics es 50. Las estimaciones de cardinalidad anteriores suponen que los valores de las columnas Make y Model son independientes unos de otros. El optimizador de consultas anterior estima que hay 10 Honda Civics (.05 *.20 \* 1000 filas = 10 filas).  
  
```  
SELECT year, purchase_price FROM dbo.Cars WHERE Make = 'Honda' AND Model = 'Civic';  
```  
  
 Este comportamiento ha cambiado. Ahora, las nuevas estimaciones de cardinalidad suponen que las columnas Make y Model tienen *alguna* correlación. El optimizador de consultas estima una cardinalidad mayor al agregar un componente exponencial a la ecuación de estimación. El optimizador de consultas estima ahora que 22,36 filas (.05 * SQRT(.20) \* 1000 filas = 22,36 filas) coinciden con el predicado. En este escenario y en esta distribución de datos específica, 22,36 filas es un valor más cercano a las 50 filas reales que devolverá la consulta.  
  
 Tenga en cuenta que la nueva lógica del estimador de cardinalidad ordena las selectividades de predicado y aumenta el exponente. Por ejemplo, si las selectividades de predicado fueran.05,.20 y. 25, la estimación de cardinalidad sería (.05 * SQRT(.20) \* SQRT(SQRT(.25))).  
  
### <a name="example-c-new-cardinality-estimates-assume-filtered-predicates-on-different-tables-are-independent"></a>Ejemplo C. Las nuevas estimaciones de cardinalidad suponen que los predicados filtrados en tablas diferentes son independientes.  
 En este ejemplo, el estimador de cardinalidad anterior supone que los filtros de predicado s.type y r.date están correlacionados. Sin embargo, los resultados de las pruebas en cargas de trabajo modernas mostraron que los filtros de predicados en columnas de tablas diferentes no suelen estar correlacionados entre sí.  
  
```  
SELECT s.ticket, s.customer, r.store FROM dbo.Sales AS s CROSS JOIN dbo.Returns AS r  
WHERE s.ticket = r.ticket AND s.type = 'toy' AND r.date = '2013-12-19';  
```  
  
 Este comportamiento ha cambiado. Ahora, la nueva lógica del estimador de cardinalidad supone que s.type no está correlacionado con r.date. En la práctica, la suposición es que se devuelven juguetes todos los días y no solo un día determinado. En este caso, las nuevas estimaciones de cardinalidad serán un número menor que las estimaciones de cardinalidad anteriores.  
  
## <a name="see-also"></a>Vea también  
 [Supervisión y optimización del rendimiento](monitor-and-tune-for-performance.md)  
  
  
