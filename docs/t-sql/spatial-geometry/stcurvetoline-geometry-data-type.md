---
title: STCurveToLine (tipo de datos geometry) | Documentos de Microsoft
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
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5950ba5609fdd34008c051166f089cf3433890d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine (tipo de datos de geometría)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve una aproximación poligonal de un **geometry** instancia que contiene los segmentos de arco circular.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentarios  
 Devuelve una instancia vacía **GeometryCollection**instancia para vacío **geometry** variables y devuelve la instancia **NULL** para que no se ha inicializado **geometry** variables.  
  
 Depende de la aproximación poligonal devuelta por el método devuelve el **geometry** instancia que utiliza para llamar al método:  
  
-   Devuelve un **LineString** de instancia para una **CircularString** o **CompoundCurve** instancia.  
  
-   Devuelve un **polígono** de instancia para una **CurvePolygon** instancia.  
  
-   Devuelve una copia de la **geometry** si esa instancia no es un **CircularString**, **CompoundCurve**, o **CurvePolygon** instancia . Por ejemplo, el `STCurveToLine` método devuelve un **punto** de instancia para una **geometry** instancia que es un **punto** instancia.  
  
 A diferencia de la especificación SQL/MM, el `STCurveToLine` el método no usa los valores de coordenada z para calcular la aproximación poligonal. El método omite los valores de coordenada z está presentes en la llamada a **geometry** instancia.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. Usar una variable geometry sin inicializar y una instancia vacía  
 En el ejemplo siguiente, la primera **seleccione** instrucción utiliza una sin inicializar **geometry** instancia para llamar a la `STCurveToLine` método y el segundo **seleccione** instrucción utiliza vacío **geometry** instancia. Por lo tanto, el método devuelve **NULL** a la primera instrucción y un **GeometryCollection** colección a la segunda instrucción.  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. Utilizar una instancia de LineString  
 El **seleccione** instrucción en el ejemplo siguiente utiliza un **LineString** instancia para llamar al método STCurveToLine. Por lo tanto, el método devuelve un **LineString** instancia.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. Utilizar una instancia de CircularString  
 La primera **seleccione** instrucción en el ejemplo siguiente utiliza un **CircularString** instancia para llamar al método STCurveToLine. Por lo tanto, el método devuelve un **LineString** instancia. Esto **seleccione** instrucción también compara las longitudes de las dos instancias, que son aproximadamente iguales.  Por último, el segundo **seleccione** instrucción devuelve el número de puntos para cada instancia.  Devuelve solo los 5 puntos para la **CircularString** instancia pero 65 puntos para la **LineString**instancia.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. Utilizar una instancia de CurvePolygon  
 El **seleccione** instrucción en el ejemplo siguiente utiliza un **CurvePolygon** instancia para llamar al método STCurveToLine. Por lo tanto, el método devuelve un **polígono** instancia.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>Vea también  
 [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  

