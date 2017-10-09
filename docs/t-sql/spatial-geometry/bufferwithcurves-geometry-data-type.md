---
title: BufferWithCurves (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a88ea4010ec1cfd48661b34e990634fe371141f3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves (tipo de datos Geometry)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Devuelve un **geometry** instancia que representa el conjunto de todos los puntos cuya distancia desde la llamada a **geometry** instancia es menor o igual que el *distancia* parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distancia*  
 Es un **float** que indica la distancia máxima a la que apunta forman el búfer pueden estar desde el **geometry** instancia.  
  
## <a name="return-types"></a>Tipos devueltos  
Tipo de valor devuelto de SQL Server: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Excepciones  
 Los siguientes criterios, se producirán un **ArgumentException**.  
  
-   No se pasa ningún parámetro al método, como `@g.BufferWithCurves()`  
  
-   Se pasa al método un parámetro no numérico, como `@g.BufferWithCurves('a')`  
  
-   **NULL** se pasa al método, como`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Comentarios  
 En la siguiente ilustración se muestra un ejemplo de una instancia de geometría devuelta por este método.  
  
 ![BufferedCurve](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 En la siguiente tabla se muestran los resultados devueltos para distintos valores de distancia.  
  
|Valor de distancia|Dimensiones de tipo|Tipo espacial devuelto|  
|--------------------|---------------------|---------------------------|  
|distancia < 0|Cero o uno|Vacía **GeometryCollection** instancia|  
|distancia < 0|Dos o más|A **CurvePolygon** o **GeometryCollection** instancia con un búfer negativo. **Nota:** un búfer negativo puede crear vacío **GeometryCollection**|  
|distancia = 0|Todas las dimensiones|Copia de la llamada **geometry** instancia|  
|distancia > 0|Todas las dimensiones|**CurvePolygon** o **GeometryCollection** instancia|  
  
> [!NOTE]  
>  Puesto que *distancia* es un **float**, un valor muy pequeño puede igualarse a cero en los cálculos. Si sucede esto, una copia de la llamada a **geometry** se devuelve la instancia. Vea [float y real &#40; Transact-SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Un búfer negativo quita todos los puntos incluidos en la distancia especificada del límite de la geometría. En la siguiente ilustración se muestra un búfer negativo como el área del círculo sombreada en claro. La línea de puntos es el límite del polígono original y la línea continua es el límite del polígono resultante.  
  
 Si un **cadena** parámetro se pasa al método, a continuación, se convertirá en un **float** o producirá un `ArgumentException`.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geometry-instance"></a>A. Llamada a BufferWithCurves() con un valor de parámetro < 0 en una instancia de geometría de una dimensión  
 En el siguiente ejemplo se devuelve una instancia de `GeometryCollection` vacía:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(-1).ToString(); 
 ```
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geometry-instance"></a>B. Llamada a BufferWithCurves() con un valor de parámetro < 0 en una instancia de geometría de dos dimensiones  
 En el siguiente ejemplo se devuelve una instancia de `CurvePolygon` con un búfer negativo:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Llamada a BufferWithCurves() con un valor de parámetro < 0 que devuelve una instancia de GeometryCollection vacía  
 En el ejemplo siguiente se muestra lo que sucede cuando el *distancia* parámetro es igual a -2:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Esto **seleccione** instrucción devuelve`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Llamada a BufferWithCurves() con un valor de parámetro = 0  
 En el ejemplo siguiente se devuelve una copia de la llamada a **geometry** instancia:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Llamada a BufferWithCurves() con un valor de parámetro distinto de cero que es sumamente pequeño  
 En el ejemplo siguiente se devuelve también una copia de la llamada a **geometry** instancia:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 DECLARE @distance float = 1e-20; 
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Llamada a BufferWithCurves() con un valor de parámetro > 0  
 En el ejemplo siguiente se devuelve una instancia de `CurvePolygon`:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
  
### <a name="g-passing-a-valid-string-parameter"></a>G. Se pasa un parámetro de cadena válido  
 En el ejemplo siguiente se devuelve la misma instancia de `CurvePolygon` mencionada anteriormente, pero se pasa un parámetro de cadena al método:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves('2').ToString();
 ```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. Se pasa un parámetro de cadena no válido  
 En el siguiente ejemplo se producirá un error:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)' 
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 Observe que en los dos ejemplos anteriores se pasa un literal de cadena al método `BufferWithCurves()`. El primer ejemplo funciona porque el literal de cadena se puede convertir en un valor numérico. Sin embargo, el segundo ejemplo inicia una excepción `ArgumentException`.  
  
### <a name="i-calling-bufferwithcurves-on-multipoint-instance"></a>I. Llamada a BufferWithCurves() en una instancia de tipo MultiPoint  
 En el siguiente ejemplo se devuelven dos instancias de `GeometryCollection` y una de `CurvePolygon`:  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.BufferWithCurves(1).ToString(); 
 SELECT @g.BufferWithCurves(1.5).ToString(); 
 SELECT @g.BufferWithCurves(1.6).ToString();
 ```  
  
 Las dos primeras **seleccione** instrucciones devuelven un `GeometryCollection` instancia porque el parámetro *distancia* es menor o igual a 1/2, la distancia entre los dos puntos (1 1) y (1 4). La tercera **seleccione** instrucción devuelve un `CurvePolygon` instancia porque las instancias almacenadas en búfer de los dos puntos (1 1) y (1 4) se superponen.  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 

