---
title: STCurveN (tipo de datos geography) | Documentos de Microsoft
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
- STCurveN
- STCurveN_TSQL
dev_langs: TSQL
helpviewer_keywords: STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a529bc1e3b818189f86d5e161b344291a975ec2c
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="stcurven-geography-data-type"></a>STCurveN (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve la curva especificada desde un **geography** instancia que es un **LineString**, **CircularString**, o **CompoundCurve**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Es un **int** expresión entre 1 y el número de curvas de la **geography** instancia.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Excepciones  
 Si n < 1 un **ArgumentOutOfRangeException** se produce.  
  
## <a name="remarks"></a>Comentarios  
 **NULL** se devuelve cuando se produce los siguientes criterios.  
  
-   El **geography** instancia se declara, pero no se crea una instancia  
  
-   El **geography** instancia está vacía  
  
-   n supera el número de curvas de la **geography** instancia (vea [STNumCurves &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   La dimensión para la **geography** instancia no es igual a (vea [STDimension &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. Usar STCurveN() en una CircularString  
 En el ejemplo siguiente se devuelve la segunda curva en una **CircularString** instancia:  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 El ejemplo devuelve  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. Usar STCurveN() en una CompoundCurve  
 En el ejemplo siguiente se devuelve la segunda curva en una **CompoundCurve** instancia:  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 El ejemplo devuelve  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. Usar STCurveN() en una CompoundCurve que tiene tres CircularStrings  
 En el ejemplo siguiente se usa un **CompoundCurve** instancias que combina tres independiente **CircularString** secuencia como en el ejemplo anterior de la curva de instancias en el mismo:  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 El ejemplo devuelve  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()` devuelve los mismos resultados sea cual sea el formato de Well-known text (WKT) que se utilice.  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. Comprobar la validez antes de llamar a STCurve()  
 En el ejemplo siguiente se muestra cómo asegurarse de que  *n*  sea válido antes de llamar al método STCurveN():  
  
```
 DECLARE @g geography;  
 DECLARE @n int;  
 SET @n = 2;  
 SET @g = geography::Parse('LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
  ```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
