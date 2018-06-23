---
title: CurvePolygon | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e000a1d8-a049-4542-bfeb-943fd6ab3969
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a772fba6776195e914d9e4109a7973f355f3a270
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201124"
---
# <a name="curvepolygon"></a>CurvePolygon
  Un `CurvePolygon` es una superficie cerrada topológicamente definida por un anillo de límite exterior y cero o más anillos interiores  
  
> [!IMPORTANT]  
>  Para obtener una descripción detallada y ejemplos de las características espaciales introducidas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluido el `CurvePolygon` subtipo, descargue las notas del producto, [nuevas características espaciales de SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Los siguientes criterios definen atributos de un `CurvePolygon` instancia:  
  
-   El límite de la instancia de `CurvePolygon` se define mediante el anillo exterior y todos los anillos interiores.  
  
-   El interior de la instancia de `CurvePolygon` es el espacio entre el anillo exterior y todos los anillos interiores.  
  
 A `CurvePolygon` instancia difiere de un `Polygon` instancia en que un `CurvePolygon` instancia puede contener los siguientes segmentos de arco circular: `CircularString` y `CompoundCurve`.  
  
## <a name="compoundcurve-instances"></a>Instancias de CompoundCurve  
 Ilustración siguiente muestra `CurvePolygon` cifras:  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Para una `CurvePolygon` instancia que se acepte, tiene que estar vacía o contener solo los anillos de arco circular que se aceptan. Un anillo de arco circular aceptado cumple los siguientes requisitos.  
  
1.  Es una instancia de `LineString`, `CircularString` o `CompoundCurve` aceptada. Para obtener más información sobre instancias aceptadas, vea [LineString](linestring.md), [CircularString](circularstring.md)y [CompoundCurve](compoundcurve.md).  
  
2.  Tiene cuatro puntos como mínimo.  
  
3.  Los puntos inicial y final tienen las mismas coordenadas X e Y.  
  
    > [!NOTE]  
    >  Se omiten los valores Z y M.  
  
 En el ejemplo siguiente se muestra aceptado `CurvePolygon` instancias.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0, 0 0))';  
DECLARE @g3 geometry = 'CURVEPOLYGON((0 0 1, 0 0 2, 0 0 3, 0 0 3))'  
DECLARE @g4 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
DECLARE @g5 geography = 'CURVEPOLYGON((-122.3 47, 122.3 -47, 125.7 -49, 121 -38, -122.3 47))';  
```  
  
 `@g3` aunque los puntos inicial y final tengan distintos valores Z porque se omiten los valores Z. Se acepta `@g5` aunque la instancia del tipo `geography` no sea válida.  
  
 Los ejemplos siguientes inician `System.FormatException`.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON((0 5, 0 0, 0 0, 0 0))';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0))';  
```  
  
 `@g1` no se acepta porque los puntos inicial y final no tienen el mismo valor Y. `@g2` no se acepta porque el anillo no tiene suficientes puntos.  
  
### <a name="valid-instances"></a>Instancias válidas  
 Para una `CurvePolygon` instancia sea válida los anillos exterior e interiores deben cumplir los siguientes criterios:  
  
1.  Solo pueden tocar en puntos de tangencia únicos.  
  
2.  No pueden cruzarse entre sí.  
  
3.  Cada anillo debe contener cuatro puntos como mínimo.  
  
4.  Cada anillo debe ser un tipo de curva aceptable.  
  
 `CurvePolygon` instancias también tienen que cumplir criterios concretos en función de si están `geometry` o `geography` tipos de datos.  
  
#### <a name="geometry-data-type"></a>Tipo de datos geometry  
 Una instancia de **geometryCurvePolygon** válida debe tener los siguientes atributos:  
  
1.  Todos los anillos interiores deben estar contenidos en el anillo exterior.  
  
2.  Puede tener varios anillos interiores, pero un anillo interior no puede contener otro anillo interior.  
  
3.  Ningún anillo puede cruzarse consigo mismo ni con otros.  
  
4.  Los anillos solo pueden tocar en puntos de tangencia únicos (el número de puntos donde el contacto de los anillos debe ser finito).  
  
5.  El interior del polígono debe estar conectado.  
  
 En el siguiente ejemplo se muestran instancias válidas de **geometryCurvePolygon** .  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
 Las instancias de CurvePolygon tienen las mismas reglas de validez que las de Poligon con la excepción de que las instancias de CurvePolygon pueden aceptar los nuevos tipos de segmento de arco circular. Para obtener más ejemplos de instancias que son válidas o que no lo son, vea [Polygon](polygon.md).  
  
#### <a name="geography-data-type"></a>Tipo de datos geography  
 Una instancia de **geographyCurvePolygon** válida debe tener los siguientes atributos:  
  
1.  El interior del polígono está conectado siguiendo la regla de la izquierda.  
  
2.  Ningún anillo puede cruzarse consigo mismo ni con otros.  
  
3.  Los anillos solo pueden tocar en puntos de tangencia únicos (el número de puntos donde el contacto de los anillos debe ser finito).  
  
4.  El interior del polígono debe estar conectado.  
  
 En el siguiente ejemplo se muestra una instancia de CurvePolygon geography válida.  
  
```  
DECLARE @g geography = 'CURVEPOLYGON((-122.3 47, 122.3 47, 125.7 49, 121 38, -122.3 47))';  
SELECT @g.STIsValid();  
```  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-curvepolygon"></a>A. Crear una instancia de una instancia de geometry con un CurvePolygon vacío  
 En este ejemplo se muestra cómo crear una instancia de `CurvePolygon` vacía:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-with-a-curvepolygon-in-the-same-statement"></a>B. Declarar y crear instancias de una instancia geometry con un CurvePolygon en la misma instrucción  
 Este fragmento de código muestra cómo declarar e inicializar una instancia geometry con un `CurvePolygon` en la misma instrucción:  
  
```tsql  
DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))'  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-curvepolygon"></a>C. Crear instancias de una instancia de geography con un CurvePolygon  
 Este fragmento de código muestra cómo declarar e inicializar un `geography` instancia con un `CurvePolygon`:  
  
```tsql  
DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-curvepolygon-with-only-an-exterior-bounding-ring"></a>D. Almacenar un CurvePolygon con solo un anillo de límite exterior  
 En este ejemplo se muestra cómo almacenar un círculo simple en una instancia de `CurvePolygon` (solo se utiliza un anillo de límite exterior para definir el círculo):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
### <a name="e-storing-a-curvepolygon-containing-interior-rings"></a>E. Almacenar un CurvePolygon que contiene anillos interiores  
 En este ejemplo se crea un anillo en una `CurvePolygon` instancia (un límite de anillo y un anillo interior exterior se usa para definir el anillo):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
 Este ejemplo muestra ambos válido `CurvePolygon` instancia y una instancia no válida al usar los anillos interiores:  
  
```tsql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (-2 2, 2 2, 2 -2, -2 -2, -2 2))');  
IF @g1.STIsValid() = 1  
  BEGIN  
     SELECT @g1.STArea();  
  END  
SET @g2 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (0 5, 5 0, 0 -5, -5 0, 0 5))');  
IF @g2.STIsValid() = 1  
  BEGIN  
     SELECT @g2.STArea();  
  END  
SELECT @g1.STIsValid() AS G1, @g2.STIsValid() AS G2;  
```  
  
 @g1 y @g2 usan el mismo anillo de límite exterior: un círculo con un radio de 5 y los dos usan un cuadrado para un anillo interior.  Sin embargo, la instancia de @g1 es válida, pero la instancia de @g2 no lo es.  La razón de que @g2 no sea válida es que el anillo interior divide el espacio interior limitado por el anillo exterior en cuatro regiones independientes.  El siguiente dibujo muestra lo que ha sucedido:  
  
## <a name="see-also"></a>Vea también  
 [Polygon](polygon.md)   
 [CircularString](circularstring.md)   
 [CompoundCurve](compoundcurve.md)   
 [Referencia de los métodos del tipo de datos geometry](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql)   
 [Referencia de los métodos del tipo de datos geography](/sql/t-sql/spatial-geography/spatial-types-geography)   
 [Información general de los tipos de datos espaciales](spatial-data-types-overview.md)  
  
  
