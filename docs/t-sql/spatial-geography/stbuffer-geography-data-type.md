---
title: STBuffer (tipo de datos geography) | Documentos de Microsoft
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
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs: TSQL
helpviewer_keywords: STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4f0cf2e9d8f4514f9017da8f75a8fa15d5dcb324
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="stbuffer-geography-data-type"></a>STBuffer (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve un objeto de geography que representa la unión de todos los puntos cuya distancia desde una **geography** instancia es menor o igual que un valor especificado.  
  
 Admite el método de tipo de este datos geography **FullGlobe** instancias o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distancia*  
 Es un valor de tipo **float** (**doble** en .NET Framework) especifica la distancia desde la **geography** instancia alrededor de la cual se puede calcular el búfer.  
  
 La distancia máxima del búfer no puede superar 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 circunferencia Terráquea) o todo el globo terráqueo.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 STBuffer() calcula un búfer de la misma manera que [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md), especificando *tolerancia* = ABS (distancia) \* .001 y *relativa*  =  **false**.  
  
 Un búfer negativo quita todos los puntos dentro de la distancia especificada del límite de la **geography** instancia.  
  
 `STBuffer()`devolverá un **FullGlobe** instancia en ciertos casos; por ejemplo, `STBuffer()` devuelve un **FullGlobe** instancia cuando la distancia del búfer es mayor que la distancia desde el Ecuador hasta los polos. Un búfer no puede superar el globo terráqueo completo.  
  
 Este método producirá una **ArgumentException** en **FullGlobe** instancias donde la distancia del búfer supera la limitación siguiente:  
  
 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 circunferencia Terráquea)  
  
 El límite de distancia máxima permite que la construcción del búfer sea lo más flexible posible.  
  
 El error entre el búfer teórico y calculada es max (tolerancia a errores, extensiones * 1.E-7) donde tolerancia = distancia \* .001. Para obtener más información sobre extensiones, consulte [referencia de método de tipo de datos geography](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea un `LineString``geography` instancia. A continuación, se usa `STBuffer()` para devolver la región que se encuentra en un radio de 1 metro de la instancia.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [BufferWithTolerance &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
