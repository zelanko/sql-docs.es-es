---
title: CurveToLineWithTolerance (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 34cb0cbe98bd0afd9eb1e3183839984799df7718
ms.sourcegitcommit: c61c7b598aa61faa34cd802697adf3a224aa7dc4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56154840"
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve una aproximación poligonal de una instancia de **geography** que contiene segmentos de arco circulares.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
_tolerance_  
Expresión **double** que define el error máximo entre el segmento del arco circular original y su aproximación lineal.  
  
_relative_  
Expresión **bool** que indica si se va a usar un máximo relativo para la desviación. Si relative está establecido en falso (0), se establece un máximo absoluto para la desviación que puede tener una aproximación lineal. Cuando relative es true (1), la tolerancia se calcula como un producto del parámetro de tolerancia y el diámetro del cuadro de límite para el objeto espacial.  
  
## <a name="return-types"></a>Tipos devueltos  
Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Excepciones  
Si se establece la tolerancia <= 0, se produce una excepción **ArgumentOutOfRange**.  
  
## <a name="remarks"></a>Notas  
Este método permite especificar una cantidad de tolerancia a errores para el valor **LineString** resultante.  
  
El método **CurveToLineWithTolerance** devolverá una instancia de **LineString** para una instancia de **CircularString** o **CompoundCurve** y una instancia de **Polygon** para una instancia de **CurvePolygon**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. Utilizar valores de tolerancia diferentes en una instancia de CircularString  
En el siguiente ejemplo se muestra cómo establecer la tolerancia afecta a la instancia de `LineString` devuelta desde una instancia de `CircularString`:  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>b. Utilizar el método en una instancia de MultiLineString que contiene un LineString  
En el siguiente ejemplo se muestra lo que se devuelve de una instancia de `MultiLineString` que solo contiene una instancia de `LineString`:  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649))');  
SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. Utilizar el método en una instancia de MultiLineString que contiene varios LineString  
En el siguiente ejemplo se muestra lo que se devuelve de una instancia de `MultiLineString` que contiene más de una instancia de `LineString`:  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649),(-123.358 47.653, -123.348 47.649))');  
SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. Establecer relative en true para invocar una instancia de CurvePolygon  
En el siguiente ejemplo se usa una instancia de `CurvePolygon` para llamar a `CurveToLineWithTolerance()` con *relative* establecido en true:  
  
```
DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
```  
  
## <a name="see-also"></a>Consulte también  
[Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
