---
title: CurveToLineWithTolerance (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e9f0f517bb9685c308999e8f3dca719cc145ed24
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36254767"
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una aproximación poligonal de una instancia de **geography** que contiene segmentos de arco circulares.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerance*  
 Expresión **double** que define el error máximo entre el segmento del arco circular original y su aproximación lineal.  
  
 *relative*  
 Expresión **bool** que indica si se va a usar un máximo relativo para la desviación. Cuando relative está establecido en falso (0), se establece un máximo absoluto para la desviación que puede tener una aproximación lineal.  Cuando relative está establecido en true (1), la tolerancia se calcula como un producto del parámetro de tolerancia y el diámetro del cuadro de límite para el objeto espacial.  
  
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
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. Utilizar el método en una instancia de MultiLineString que contiene un LineString  
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
  
## <a name="see-also"></a>Ver también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
