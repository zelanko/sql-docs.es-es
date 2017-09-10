---
title: BufferWithTolerance (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: feaa401cfd6e2077035d164412941392412011ae
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un objeto geométrico que representa la unión de todos los valores cuya distancia desde una **geography** instancia es menor o igual que un valor especificado, permitiendo una tolerancia especificada.  
  
 Admite el método de tipo de este datos geography **FullGlobe** instancias o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distancia*  
 Es un **float** expresión que especifica la distancia desde la **geography** instancia alrededor de la cual se puede calcular el búfer.  
  
 La distancia máxima del búfer no puede superar 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 circunferencia Terráquea) o todo el globo terráqueo.  
  
 *tolerancia*  
 Es un **float** expresión que especifica la tolerancia de la distancia de búfer.  
  
 El *tolerancia* valor hace referencia a la variación máxima en la distancia de búfer ideal para la aproximación lineal devuelta.  
  
 Por ejemplo, la distancia de búfer ideal de un punto es un círculo, pero un círculo debe conseguirse de forma aproximada mediante un polígono. Cuanto más pequeña sea la tolerancia, más puntos tendrá el polígono, lo que aumenta la complejidad del resultado, pero disminuye el error.  
  
 El límite mínimo es el 0,1 por ciento de la distancia, y cualquier tolerancia menor se redondeará hasta el límite mínimo.  
  
 *relativa*  
 Es un **bits** especifica si la *tolerancia* valor es relativo o absoluto. Si 'TRUE' o 1, la tolerancia es relativa y se calcula como el producto de la *tolerancia* parámetro y la magnitud angular \* radio Ecuatorial de la elipsoide. Si 'FALSE' o 0, la tolerancia es absoluta y *tolerancia* valor es la variación máxima absoluta en la distancia de búfer ideal para la aproximación lineal devuelta.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 Este método producirá una **ArgumentException** si la *distancia* no es un número (NAN), o si *distancia* es infinito positivo o negativo.  Este método también producirá un **ArgumentException** si *tolerancia* es cero (0), no es un número (NaN), infinito negativo o positivo o negativo.  
  
 `STBuffer()`devolverá un **FullGlobe** instancia en ciertos casos; por ejemplo, `STBuffer()` devuelve un **FullGlobe** instancia de dos polos cuando la distancia del búfer es mayor que la distancia desde el Ecuador a los polos.  
  
 Este método producirá una **ArgumentException** en **FullGlobe** instancias donde la distancia del búfer supera la limitación siguiente:  
  
 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 circunferencia Terráquea)  
  
 El error entre el búfer teórico y calculada es max (tolerancia a errores, extensiones \* 1.E-7) donde la tolerancia es el valor de la *tolerancia* parámetro. Para obtener más información sobre extensiones, consulte [referencia de método de tipo de datos geography](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
 Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` y se usa `BufferWithTolerance()` para obtener un búfer aproximado a su alrededor.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [STBuffer &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
 [Métodos extendidos en instancias de Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
