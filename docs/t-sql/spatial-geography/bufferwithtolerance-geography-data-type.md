---
title: BufferWithTolerance (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 2e3208d3a70c0970e34e84723c5a95e85c55e859
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937271"
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un objeto geométrico que representa la unión de todos los valores de puntos cuya distancia desde una instancia de **geography** es menor o igual que un valor especificado, permitiendo una tolerancia determinada.  
  
Este método del tipo de datos geography admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
_distance_  
Es una expresión **float** que especifica la distancia desde la instancia de **geography** en torno a la que se va a calcular el búfer.  
  
La distancia máxima del búfer no puede ser superior a 0,999 \* _π_ * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 circunferencia terráquea) o todo el globo terráqueo.  
  
_tolerance_  
Es una expresión **float** que especifica la tolerancia de la distancia del búfer.  
  
El valor _tolerance_ hace referencia a la variación máxima en la distancia del búfer idónea para la aproximación lineal devuelta.  
  
Por ejemplo, la distancia de búfer idónea de un punto es un círculo, pero esta distancia se debe aproximar mediante un polígono. Cuanto menor sea la tolerancia, más puntos tendrá el polígono. Este resultado aumenta la complejidad del resultado, pero reduce el error.  
  
El límite mínimo es el 0,1 por ciento de la distancia, y cualquier tolerancia menor se redondeará hasta el límite mínimo.  
  
_relative_  
Es un valor **bit** que especifica si el valor _tolerance_ es relativo o absoluto. Si el valor es "TRUE" o 1, la tolerancia es relativa. Este valor es el producto del parámetro _tolerance_ y la extensión angular \* el radio ecuatorial de la elipsoide. La tolerancia es absoluta si el valor es "FALSE" o 0. El valor de _tolerance_ es la variación máxima absoluta en la distancia del búfer idónea para la aproximación lineal devuelta.  
  
## <a name="return-types"></a>Tipos devueltos  
Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Notas  
Este método produce una excepción **ArgumentException** si _distance_ no es un número (NAN) o si _distance_ es infinito positivo o negativo.  Este método también produce una excepción **ArgumentException** si _tolerance_ es cero (0), no es un número (NAN), es negativo o si es infinito positivo o negativo.  
  
`STBuffer()` devuelve una instancia de **FullGlobe** en determinados casos; por ejemplo, `STBuffer()` devuelve una instancia de **FullGlobe** en dos polos cuando la distancia del búfer es mayor que la distancia desde el ecuador a los polos.  
  
Este método produce una excepción **ArgumentException** en las instancias de **FullGlobe** donde la distancia del búfer supera la siguiente limitación:  
  
0,999 \* _π_ * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 circunferencia terráquea)  
  
El error entre el búfer teórico y el calculado es max(tolerance, extents \* 1.E-7), donde tolerance es el valor del parámetro _tolerance_. Para más información sobre las extensiones, vea [Referencia de los métodos del tipo de datos geography](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
Este método no es exacto.  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se crea una instancia de `Point` y se usa `BufferWithTolerance()` para obtener un búfer aproximado a su alrededor.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
[STBuffer &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
[Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
