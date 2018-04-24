---
title: Reduce (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b8b309fa04435b319fc1e969dbc0830c3a4b515e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="reduce-geometry-data-type"></a>Reduce (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una aproximación de la instancia de **geometry** especificada que se genera al ejecutar una extensión del algoritmo de Douglas-Peucker en la instancia con la tolerancia indicada.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerance*  
 Es un valor de tipo **float**. *tolerancia* es la tolerancia que se usa como entrada para el algoritmo de aproximación.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Notas  
 Para los tipos de colección, este algoritmo funciona independientemente en cada tipo **geometry** contenido en la instancia.  
  
 Este algoritmo no modifica las instancias de **Point**.  
  
 En las instancias de **LineString**, **CircularString** y **CompoundCurve**, el algoritmo de aproximación conserva los puntos iniciales y finales originales de la instancia y va agregando el punto de la instancia original que más se desvía del resultado hasta que ningún punto se desvíe más que la tolerancia especificada.  
  
 `Reduce()` devuelve una instancia de **LineString**, **CircularString** o **CompoundCurve** para las instancias de **CircularString**.  `Reduce()` devuelve una instancia de **CompoundCurve** o **LineString** para las instancias de **CompoundCurve**.  
  
 En las instancias de **Polygon**, el algoritmo de aproximación se aplica independientemente a cada anillo. El método generará una excepción `FormatException` si la instancia de **Polygon** devuelta no es válida; por ejemplo, se crea una instancia de **MultiPolygon** no válida si se aplica `Reduce()` para simplificar cada anillo de la instancia y los anillos resultantes se superponen.  En las instancias de **CurvePolygon** con un anillo exterior y sin anillos interiores, `Reduce()` devuelve una instancia de **CurvePolygon**, **LineString** o **Point**.  Si **CurvePolygon** tiene anillos interiores, se devuelve una instancia de **CurvePolygon** o **MultiPoint**.  
  
 Cuando se detecta un segmento de arco circular, el algoritmo de aproximación comprueba si se puede aproximar al arco su cuerda en la mitad de la tolerancia indicada.  Si la cuerda satisface este criterio, la cuerda reemplaza el arco circular en los cálculos. Si no satisface este criterio, se conserva el arco circular y se aplica el algoritmo de aproximación a los segmentos restantes.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-reduce-to-simplify-a-linestring"></a>A. Usar Reduce() para simplificar LineString  
 En el ejemplo siguiente se crea una instancia sencilla de `LineString` y se utiliza `Reduce()` para simplificar la instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0, 2 1, 3 0, 4 1)', 0);  
SELECT @g.Reduce(.75).ToString();  
```  
  
### <a name="b-using-reduce-with-varying-tolerance-levels-on-a-circularstring"></a>B. Usar Reduce() con niveles de tolerancia que varían en CircularString  
 En el ejemplo siguiente se usa `Reduce()` con tres niveles de tolerancia en una instancia de **CircularString**:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0)'; 
 SELECT @g.Reduce(5).ToString(); 
 SELECT @g.Reduce(15).ToString(); 
 SELECT @g.Reduce(16).ToString();
 ```  
  
 En este ejemplo se produce la siguiente salida:  
  
 ```
 CIRCULARSTRING (0 0, 8 8, 16 0, 20 -4, 24 0) 
 COMPOUNDCURVE (CIRCULARSTRING (0 0, 8 8, 16 0), (16 0, 24 0)) 
 LINESTRING (0 0, 24 0)
 ```  
  
 Cada una de las instancias devueltas contiene los extremos (0 0) y (24 0).  
  
### <a name="c-using-reduce-with-varying-tolerance-levels-on-a-compoundcurve"></a>C. Usar Reduce() con niveles de tolerancia que varían en CompoundCurve  
 En el ejemplo siguiente se usa `Reduce()` con dos niveles de tolerancia en una instancia de **CompoundCurve**:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 En este ejemplo, observe que la segunda instrucción **SELECT** devuelve la instancia de **LineString**: `LineString(0 0, 16 0)`.  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>Mostrar un ejemplo en el que se pierdan los puntos inicial y final originales  
 En el siguiente ejemplo se muestra cómo la instancia resultante no conserva los puntos inicial y final originales. Esto se produce porque si se conservan los puntos inicial y final originales, el resultado sería una instancia de **LineString** no válida.  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de geometría estáticos ampliados](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

