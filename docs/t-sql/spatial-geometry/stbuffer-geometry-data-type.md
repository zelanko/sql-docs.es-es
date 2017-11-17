---
title: STBuffer (tipo de datos geometry) | Documentos de Microsoft
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
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 87ad6ea01e471cf1ec407f0b8372300d07f0118f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stbuffer-geometry-data-type"></a>STBuffer (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un objeto geométrico que representa la unión de todos los puntos cuya distancia desde una **geometry** instancia es menor o igual que un valor especificado.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distancia*  
 Es un valor de tipo **float** (**doble** en .NET Framework) especifica la distancia desde la instancia de geometry alrededor de la cual se puede calcular el búfer.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentarios  
 `STBuffer()`calcula un búfer como [BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md), especificando *tolerancia* = distancia \* .001 y *relativa*  =   **false**.  
  
 Cuando *distancia* > 0, a continuación, ya sea un **polígono** o **MultiPolygon** se devuelve la instancia.  
  
> [!NOTE]  
>  Puesto que la distancia es un **float**, un valor muy pequeño puede igualarse a cero en los cálculos.  Cuando esto ocurre, una copia de la llamada a **geometry** se devuelve la instancia.  Vea [float y real &#40; Transact-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
  
 Cuando *distancia* = 0, entonces una copia de la llamada a **geometry** se devuelve la instancia.  
  
 Cuando *distancia* < 0, entonces  
  
-   vacío **GeometryCollection** instancia se devuelve cuando las dimensiones de la instancia son 0 ó 1.  
  
-   se devuelve un búfer negativo si las dimensiones de la instancia son 2 o más.  
  
    > [!NOTE]  
    >  Un búfer negativo también puede crear vacío **GeometryCollection** instancia.  
  
 Un búfer negativo quita todos los puntos incluidos en la distancia dada del límite de la geometría.  
  
 El error entre el búfer teórico y calculada es max (tolerancia a errores, extensiones * 1.E-7) donde tolerancia = distancia \* .001. Para obtener más información sobre extensiones, consulte [referencia de método de tipo de datos geometry](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calling-stbuffer-with-parametervalue--0-on-one-dimensional-geometry-instance"></a>A. Llamar a STBuffer() con parameter_value < 0 en una instancia de geometría dimensional  
 En el siguiente ejemplo se devuelve una instancia de `GeometryCollection` vacía:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="b-calling-stbuffer-with-parametervalue--0-on-a-polygon-instance"></a>B. Llamar a STBuffer() con parameter_value < 0 en una instancia de Polygon  
 En el siguiente ejemplo se devuelve una instancia de `Polygon` con un búfer negativo:  
  
```
 DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="c-calling-stbuffer-with-parametervalue--0-on-a-curvepolygon-instance"></a>C. Llamar a STBuffer() con parameter_value < 0 en una instancia de CurvePolygon  
 En el siguiente ejemplo se devuelve una instancia de `Polygon` con un búfer negativo desde una instancia de `CurvePolygon`:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
> [!NOTE]  
>  Se devuelve una instancia de `Polygon` en lugar de una instancia de `CurvePolygon`.  Para devolver un `CurvePolygon` de la instancia, consulte [BufferWithCurves &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>D. Llamar a STBuffer() con un valor de parámetro negativo que devuelve una instancia vacía  
 En el ejemplo siguiente se muestra lo que sucede cuando el *distancia* parámetro es igual a -2 para el ejemplo anterior.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-2).ToString();
 ```  
  
 Esto **seleccione** instrucción devuelve una`GEOMETRYCOLLECTION EMPTY.`  
  
### <a name="e-calling-stbuffer-with-parametervalue--0"></a>E. Llamar a STBuffer() con parameter_value = 0  
 En el siguiente ejemplo se devuelve una copia de la instancia de `geometry` que realiza la llamada:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(0).ToString();
 ```  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>F. Llamar a STBuffer() con un valor de parámetro distinto de cero que es muy pequeño  
 En el siguiente ejemplo también se devuelve una copia de la instancia de `geometry` que realiza la llamada:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.STBuffer(@distance).ToString();
 ```  
  
### <a name="g-calling-stbuffer-with-parametervalue--0"></a>G. Llamar a STBuffer() con parameter_value > 0  
 En el ejemplo siguiente se devuelve una instancia de `Polygon`:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(2).ToString();
 ```  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>H. Llamar a STBuffer() con un valor de parámetro de cadena  
 En el ejemplo siguiente se devuelve la misma instancia de `Polygon` mencionada anteriormente, pero se pasa un parámetro de cadena al método:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('2').ToString();
 ```  
  
 En el siguiente ejemplo se producirá un error:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('a').ToString();
 ```  
  
> [!NOTE]  
>  En los dos ejemplos anteriores se pasó un literal de cadena a `STBuffer()`.  El primer ejemplo funciona porque el literal de cadena se puede convertir en un valor numérico. Sin embargo, el segundo ejemplo inicia una excepción `ArgumentException`.  
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>I. Llamar a STBuffer() en una instancia de MultiPoint  
 En el siguiente ejemplo se devuelven dos instancias de `MultiPolygon` y una de `Polygon`:  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.STBuffer(1).ToString(); 
 SELECT @g.STBuffer(1.5).ToString(); 
 SELECT @g.STBuffer(1.6).ToString();
 ```  
  
 Las dos primeras **seleccione** instrucciones devuelven un `MultiPolygon` instancia porque el parámetro *distancia* es menor o igual a 1/2, la distancia entre los dos puntos (1 1) y (1 4). La tercera **seleccione** instrucción devuelve un `Polygon` instancia porque las instancias almacenadas en búfer de los dos puntos (1 1) y (1 4) se superponen.  
  
## <a name="see-also"></a>Vea también  
 [BufferWithTolerance &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [Métodos de OGC en instancias de Geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


