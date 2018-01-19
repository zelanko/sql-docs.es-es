---
title: CurveToLineWithTolerance (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs: TSQL
helpviewer_keywords: CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 497daed444f29db051ac11f6f0c2c2b87011fd80
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una aproximación poligonal de un **geography** instancia que contiene los segmentos de arco circular.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerance*  
 Es un **doble** expresión que define el error máximo entre el segmento de arco circular original y su aproximación lineal.  
  
 *relative*  
 Es un **bool** expresión que indica si se debe usar un máximo relativo para la desviación. Cuando relative está establecido en falso (0), se establece un máximo absoluto para la desviación que puede tener una aproximación lineal.  Cuando relative está establecido en true (1), la tolerancia se calcula como un producto del parámetro de tolerancia y el diámetro del cuadro de límite para el objeto espacial.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Excepciones  
 Establecer la tolerancia < = 0 se produce un **ArgumentOutOfRange** excepción.  
  
## <a name="remarks"></a>Comentarios  
 Este método permite que una cantidad de tolerancia a errores que se especifique para el resultante **LineString**.  
  
 **CurveToLineWithTolerance** método devolverá un **LineString** de instancia para una **CircularString** o **CompoundCurve** instancia y **Polígono** de instancia para una **CurvePolygon** instancia.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. Utilizar valores de tolerancia diferentes en una instancia de CircularString  
 En el ejemplo siguiente se muestra cómo establecer la tolerancia afecta a la `LineString`instancia devuelta desde un `CircularString` instancia:  
  
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
 En el ejemplo siguiente se usa un `CurvePolygon` instancia para llamar a `CurveToLineWithTolerance()` con *relativa* establecido en true:  
  
 ```
 DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
