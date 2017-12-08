---
title: CompoundCurve | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: spatial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae357f9b-e3e2-4cdf-af02-012acda2e466
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b7c1727022b049923f06225c667b4a9d0438402
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="compoundcurve"></a>CompoundCurve
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] **CompoundCurve** es una recopilación de cero o más instancias de **CircularString** o **LineString** de tipos de geometría o geografía.  
  
> [!IMPORTANT]  
>  Para obtener una descripción detallada y ejemplos de las nuevas características espaciales de esta versión, incluido el subtipo **CompoundCurve** , descargue las notas del producto [Nuevas características espaciales de SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Se puede crear una instancia vacía de **CompoundCurve** , pero para que una **CompoundCurve** sea válida debe cumplir los siguientes criterios:  
  
1.  Debe contener al menos una instancia de **CircularString** o de **LineString** .  
  
2.  La secuencia de instancias de **CircularString** o **LineString** debe ser continua.  
  
 Si una **CompoundCurve** contiene una secuencia de varias instancias de **CircularString** y **LineString** , el extremo final de cada instancia, salvo la última, debe ser el extremo inicial de la siguiente instancia de la secuencia. Esto significa que si el punto final de una instancia anterior de la secuencia es (4 3 7 2), el punto inicial para la instancia siguiente de la secuencia debe ser (4 3 7 2). Observe que los valores M (medida) y Z (elevación) para el punto también deben ser iguales. Si hay diferencia entre ambos puntos, se produce una excepción `System.FormatException` . Los puntos de una **CircularString** no tienen que tener valor Z o M. Si no se proporcionan valores Z o M para el punto final de la instancia anterior, el punto inicial de la instancia siguiente no puede incluir valores Z o M. Si el punto final para la secuencia anterior es (4 3), el punto inicial para la secuencia siguiente debe ser (4 3); no puede ser (4 3 7 2). Todos los puntos de una instancia **CompoundCurve** deben tener el mismo valor Z, o bien, ningún valor Z.  
  
## <a name="compoundcurve-instances"></a>Instancias de CompoundCurve  
 La siguiente ilustración muestra tipos válidos de **CompoundCurve** .  
  
![f278742e-b861-4555-8b51-3d972b7602bf](../../relational-databases/spatial/media/f278742e-b861-4555-8b51-3d972b7602bf.gif)  
 
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Se acepta la instancia**CompoundCurve** si es una instancia vacía o cumple los siguientes criterios.  
  
1.  Todas las instancias contenidas en la instancia **CompoundCurve** son instancias de segmento de arco circular aceptadas. Para obtener más información sobre instancias de segmento de arco circular aceptadas, vea [LineString](../../relational-databases/spatial/linestring.md) y [CircularString](../../relational-databases/spatial/circularstring.md).  
  
2.  Todos los segmentos de arco circulares contenidos en la instancia **CompoundCurve** están conectados. El primer punto de cada segmento de arco circular siguiente coincide con el último punto del segmento de arco circular precedente.  
  
    > [!NOTE]  
    >  Esto incluye las coordenadas Z y M. Por tanto, las cuatro coordenadas X, Y, Z y M deben coincidir para ambos puntos.  
  
3.  Ninguna de las instancias contenidas son instancias vacías.  
  
 El siguiente ejemplo muestra instancias aceptadas de **CompoundCurve** .  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
```  
  
 El siguiente ejemplo muestra instancias de **CompoundCurve** no aceptadas. Estas instancias producen una excepción `System.FormatException`.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING EMPTY)';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (1 0, 2 0))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Una instancia de **CompoundCurve** es válida si cumple los siguientes criterios.  
  
1.  La instancia de **CompoundCurve** es aceptada.  
  
2.  Todas las instancias de segmento de arco circular contenidas en la instancia **CompoundCurve** son instancias válidas.  
  
 En el siguiente ejemplo se muestran instancias válidas de **CompoundCurve** .  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
  
```  
  
 `@g3` es válido porque la instancia **CircularString** es válida. Para obtener más información sobre la validez de la instancia **CircularString** , vea [CircularString](../../relational-databases/spatial/circularstring.md).  
  
 El siguiente ejemplo muestra instancias de **CompoundCurve** no válidas.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4, 3 5))';  
DECLARE @g2 geometry = 'COMPOUNDCURVE((1 1, 1 1))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 2 3, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g1` no es válida porque la segunda instancia no es una instancia válida de LineString. `@g2` no es válido porque la instancia **LineString** no es válida. `@g3` no es válido porque la instancia **CircularString** no es válida. Para obtener más información sobre instancias validas de **CircularString** y **LineString** , vea [CircularString](../../relational-databases/spatial/circularstring.md) y [LineString](../../relational-databases/spatial/linestring.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-compooundcurve"></a>A. Crear una instancia de geometry con una CompoundCurve vacía  
 En el ejemplo siguiente, se muestra cómo crear una instancia vacía de `CompoundCurve` :  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-using-a-compoundcurve-in-the-same-statement"></a>B. Declarar y crear una instancia de geometry usando una CompoundCurve en la misma instrucción  
 En el siguiente ejemplo, se muestra cómo declarar e inicializar una instancia de `geometry` con una `CompoundCurve`en la misma instrucción:  
  
```tsql  
DECLARE @g geometry = 'COMPOUNDCURVE ((2 2, 0 0),CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-compoundcurve"></a>C. Crear una instancia de geography con una CompoundCurve  
 En el siguiente ejemplo se muestra cómo declarar e inicializar una instancia **geography** con un elemento `CompoundCurve`:  
  
```tsql  
DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-square-in-a-compoundcurve-instance"></a>D. Almacenar un cuadrado en una instancia de CompoundCurve  
 En el siguiente ejemplo, se muestran dos maneras diferentes de utilizar una instancia `CompoundCurve` para almacenar un cuadrado.  
  
```tsql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3), (1 3, 3 3),(3 3, 3 1), (3 1, 1 1))');  
SET @g2 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3, 3 3, 3 1, 1 1))');  
SELECT @g1.STLength(), @g2.STLength();  
```  
  
 Las longitudes de `@g1` y `@g2` son iguales. Observe en el ejemplo que una instancia de **CompoundCurve** puede almacenar una o más instancias de `LineString`.  
  
### <a name="e-instantiating-a-geometry-instance-using-a-compoundcurve-with-multiple-circularstrings"></a>E. Crear una instancia de geometry usando una CompoundCurve con varias CircularStrings  
 En el siguiente ejemplo, se muestra cómo utilizar dos instancias `CircularString` diferentes para inicializar una `CompoundCurve`.  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT @g.STLength();  
```  
  
 Produce el siguiente resultado: 12.566370… que es el equivalente de 4∏. La instancia de `CompoundCurve` del ejemplo almacena un círculo de radio 2. Ambos ejemplos de código anteriores no tuvieron que utilizar una `CompoundCurve`. Para el primer ejemplo, habría sido más fácil utilizar una instancia de `LineString` , mientras que para el segundo ejemplo habría sido más fácil una instancia de `CircularString` . Sin embargo, el ejemplo siguiente muestra un caso donde `CompoundCurve` proporciona una mejor alternativa.  
  
### <a name="f-using-a-compoundcurve-to-store-a-semicircle"></a>F. Usar una CompoundCurve para almacenar un semicírculo  
 En el siguiente ejemplo, se utiliza una instancia de `CompoundCurve` para almacenar un semicírculo.  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))');  
SELECT @g.STLength();  
```  
  
### <a name="g-storing-multiple-circularstring-and-linestring-instances-in-a-compoundcurve"></a>G. Almacenar varias instancias de CircularString y LineString en una CompoundCurve  
 En el siguiente ejemplo, se muestra cómo se pueden almacenar varias instancias de `CircularString` y `LineString` mediante una `CompoundCurve`.  
  
```tsql  
DECLARE @g geometry  
SET @g = geometry::Parse('COMPOUNDCURVE((3 5, 3 3), CIRCULARSTRING(3 3, 5 1, 7 3), (7 3, 7 5), CIRCULARSTRING(7 5, 5 7, 3 5))');  
SELECT @g.STLength();  
```  
  
### <a name="h-storing-instances-with-z-and-m-values"></a>H. Almacenar instancias con valores Z y M  
 En el siguiente ejemplo, se muestra cómo utilizar una instancia `CompoundCurve` para almacenar una secuencia de instancias `CircularString` y `LineString` con valores Z y M.  
  
```tsql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(7 5 4 2, 5 7 4 2, 3 5 4 2), (3 5 4 2, 8 7 4 2))');  
```  
  
### <a name="i-illustrating-why-circularstring-instances-must-be-explicitly-declared"></a>I. Obligación de declarar las instancias de CircularString explícitamente  
 En el siguiente ejemplo, se muestra por qué se deben declarar explícitamente las instancias de `CircularString` . El programador está intentando almacenar un círculo en una instancia de `CompoundCurve` .  
  
```tsql  
DECLARE @g1 geometry;    
DECLARE @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 2 4, 0 2))');  
SELECT 'Circle One', @g1.STLength() AS Perimeter;  -- gives an inaccurate amount  
SET @g2 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT 'Circle Two', @g2.STLength() AS Perimeter;  -- now we get an accurate amount  
```  
  
 El resultado es el siguiente:  
  
```  
Circle One11.940039…  
Circle Two12.566370…  
```  
  
 El perímetro para el círculo dos es aproximadamente 4∏, que es el valor real del perímetro. Sin embargo, el perímetro para el círculo uno es significativamente inexacto. La instancia `CompoundCurve` del círculo uno almacena un segmento de arco circular (ABC) y dos segmentos de línea (CD, DA). La instancia `CompoundCurve` tiene que almacenar dos segmentos de arco circular (ABC, CDA) para definir un círculo. Una instancia `LineString` define el segundo conjunto de puntos (4 2, 2 4, 0 2) en la instancia `CompoundCurve` del círculo uno. Es necesario declarar explícitamente una instancia `CircularString` dentro de una `CompoundCurve`.  
  
## <a name="see-also"></a>Vea también  
 [STIsValid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [STLength &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)   
 [CircularString](../../relational-databases/spatial/circularstring.md)   
 [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Punto](../../relational-databases/spatial/point.md)  
  
