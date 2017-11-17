---
title: Reducir (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6e74a2a16806741dda7171ec0327b709fb697cb9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="reduce-geometry-data-type"></a>Reduce (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una aproximación de la determinada **geometry** instancia producidos mediante la ejecución de una extensión del algoritmo de Douglas-Peucker en la instancia con la tolerancia indicada.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerancia*  
 Es un valor de tipo **float**. *tolerancia* es la tolerancia como entrada para el algoritmo de aproximación.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentarios  
 Para los tipos de colección, este algoritmo funciona independientemente en cada **geometry** contenidos en la instancia.  
  
 Este algoritmo no modifica **punto** instancias.  
  
 En **LineString**, **CircularString**, y **CompoundCurve** instancias, el algoritmo de aproximación conserva el original puntos inicial y final de la instancia, y agregando el punto de la instancia original que más se desvía del resultado hasta que no hay ningún punto se desvíe más que la tolerancia indicada.  
  
 `Reduce()`Devuelve un **LineString**, **CircularString**, o **CompoundCurve** instancia para **CircularString** instancias.  `Reduce()`Devuelve un **CompoundCurve** o **LineString** instancia para **CompoundCurve** instancias.  
  
 En **polígono** instancias, el algoritmo de aproximación se aplica independientemente a cada anillo. El método generará una `FormatException` si el valor devuelto **polígono** instancia no es válida; por ejemplo, una no válida **MultiPolygon** si se crea una instancia `Reduce()` se aplica para simplificar cada uno en la instancia de anillo y se superponen los anillos resultantes.  En **CurvePolygon** instancias con un anillo exterior y sin anillos interiores, `Reduce()` devuelve un **CurvePolygon**, **LineString**, o **punto** instancia.  Si el **CurvePolygon** tiene anillos interiores un **CurvePolygon** o **MultiPoint** se devuelve la instancia.  
  
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
 En el ejemplo siguiente se utiliza `Reduce()` con tres niveles de tolerancia en una **CircularString** instancia:  
  
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
 En el ejemplo siguiente se utiliza `Reduce()` con dos niveles de tolerancia en una **CompoundCurve** instancia:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 En este ejemplo, observe que el segundo **seleccione** instrucción devuelve el **LineString** instancia: `LineString(0 0, 16 0)`.  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>Mostrar un ejemplo en el que se pierdan los puntos inicial y final originales  
 En el siguiente ejemplo se muestra cómo la instancia resultante no conserva los puntos inicial y final originales. Esto ocurre porque si se conservan al inicio original y no válido, se crearán dos puntos finales **LineString** instancia.  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de geometría estáticos ampliados](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


