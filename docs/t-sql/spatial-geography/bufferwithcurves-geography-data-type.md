---
title: BufferWithCurves (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs: TSQL
helpviewer_keywords: BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0978418fe682728d02f7c65b5bff581154ae231c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves (tipo de datos de geografía)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve un **geography** instancia que representa el conjunto de todos los puntos cuya distancia desde la llamada a **geography** instancia es menor o igual que el *distancia* parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distance*  
 Es un **float** que indica la distancia máxima a la que apunta forman el búfer puede provenir de la instancia de geography.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Excepciones  
 Los siguientes criterios, se producirán un **ArgumentException**.  
  
-   No se pasa ningún parámetro al método: `@g.BufferWithCurves()`  
  
-   Se pasa al método un parámetro no numérico: `@g.BufferWithCurves('a')`  
  
-   **NULL** se pasa al método, como`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Comentarios  
 En la siguiente tabla se muestran los resultados devueltos para distintos valores de distancia.  
  
|Valor de distancia|Dimensiones de tipo|Tipo espacial devuelto|  
|--------------------|---------------------|---------------------------|  
|distancia < 0|Cero o uno|Vacía **GeometryCollection** instancia|  
|distancia \< 0|Dos o más|A **CurvePolygon** o **GeometryCollection** instancia con un búfer negativo.<br /><br /> Nota: Un búfer negativo puede crear vacío **GeometryCollection**|
|distancia = 0|Todas las dimensiones|Copia de la llamada **geography** instancia|  
|distancia > 0|Todas las dimensiones|**CurvePolygon** o **GeometryCollection** instancia|  
  
> [!NOTE]  
>  Puesto que *distancia* es un **float**, un valor muy pequeño puede igualarse a cero en los cálculos.  Cuando esto ocurre, a continuación, una copia de la llamada a **geography** se devuelve la instancia.  
  
 Si un **cadena** parámetro se pasa al método, a continuación, se convertirá en un **float** o producirá un `ArgumentException`.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>A. Llamada a BufferWithCurves() con un valor de parámetro < 0 en una instancia de geografía de una dimensión  
 En el siguiente ejemplo se devuelve una instancia de `GeometryCollection` vacía:  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>B. Llamada a BufferWithCurves() con un valor de parámetro < 0 en una instancia de geografía de dos dimensiones  
 En el siguiente ejemplo se devuelve una instancia de `CurvePolygon` con un búfer negativo:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Llamada a BufferWithCurves() con un valor de parámetro < 0 que devuelve una instancia de GeometryCollection vacía  
 En el ejemplo siguiente se muestra lo que sucede cuando el *distancia* parámetro es igual a -2:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Esto **seleccione** instrucción devuelve`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Llamada a BufferWithCurves() con un valor de parámetro = 0  
 En el ejemplo siguiente se devuelve una copia de la llamada a **geography** instancia:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Llamada a BufferWithCurves() con un valor de parámetro distinto de cero que es sumamente pequeño  
 En el ejemplo siguiente se devuelve también una copia de la llamada a **geography** instancia:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Llamada a BufferWithCurves() con un valor de parámetro > 0  
 En el ejemplo siguiente se devuelve una instancia de `CurvePolygon`:  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>G. Se pasa un parámetro de cadena válido  
 En el ejemplo siguiente se devuelve la misma instancia de `CurvePolygon` mencionada anteriormente, pero se pasa un parámetro de cadena al método:  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves('2').ToString();
```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. Se pasa un parámetro de cadena no válido  
 En el siguiente ejemplo se producirá un error:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)'  
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 Observe que en los dos ejemplos anteriores se pasa un literal de cadena al método `BufferWithCurves()`. El primer ejemplo funciona porque el literal de cadena se puede convertir en un valor numérico. Sin embargo, el segundo ejemplo inicia una excepción `ArgumentException`.  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
