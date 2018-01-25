---
title: BufferWithTolerance (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
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
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs: TSQL
helpviewer_keywords: BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
caps.latest.revision: "31"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1cb8520351369dad761862132211b5222c52e3ae
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un objeto geométrico que representa la unión del punto de todos los valores cuya distancia desde una **geometry** instancia es menor o igual que un valor especificado, permitiendo una tolerancia especificada.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distance*  
 Es un **float** expresión que especifica la distancia desde la **geometry** instancia alrededor de la cual se puede calcular el búfer.  
  
 *tolerance*  
 Es un **float** expresión que especifica la tolerancia de la distancia de búfer.  
  
 *Tolerancia* hace referencia a la variación máxima en la distancia de búfer ideal para la aproximación lineal devuelta.  
  
 Por ejemplo, la distancia de búfer ideal de un punto es un círculo, pero un círculo debe conseguirse de forma aproximada mediante un polígono. Cuanto más pequeña sea la tolerancia, más puntos tendrá el polígono, lo que aumenta la complejidad del resultado, pero disminuye el error.  
  
 *relative*  
 Es un **bits** especifica si la *tolerancia* valor es relativo o absoluto. Si 'TRUE' o 1, a continuación, tolerancia es relativa y se calcula como el producto de la *tolerancia* parámetro y el diámetro del cuadro de límite de la instancia. Si 'FALSE' o 0, la tolerancia es absoluta y *tolerancia* valor es la variación máxima absoluta en la distancia de búfer ideal para la aproximación lineal devuelta.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Excepciones  
 El *tolerancia* parámetro debe ser mayor que cero. Si *tolerancia* < = 0, a continuación, un `System.ArgumentOutOfRangeException` se produce.  
  
> [!NOTE]  
>  Puesto que *tolerancia* es un **float** tipo, un `System.Runtime.InteropServices.COMException` se puede producir si el valor dado para la tolerancia es muy pequeño debido a problemas de redondeo con tipos de punto flotante.  
  
## <a name="remarks"></a>Comentarios  
 Cuando *distancia* > 0, a continuación, ya sea un **polígono** o **MultiPolygon** se devuelve la instancia.  
  
> [!NOTE]  
>  Puesto que la distancia es un **float**, un valor muy pequeño puede igualarse a cero en los cálculos. Cuando esto ocurre, una copia de la llamada a **geometry** se devuelve la instancia. Vea [float y real &#40; Transact-SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Cuando *distancia* = 0, a continuación, una copia de la llamada a **geometry** se devuelve la instancia.  
  
 Cuando *distancia* < 0, a continuación,  
  
-   vacío **GeometryCollection** instancia se devuelve cuando las dimensiones de la instancia son 0 ó 1.  
  
-   Se devuelve un búfer negativo si las dimensiones de la instancia son dos o más.  
  
    > [!NOTE]  
    >  Un búfer negativo también puede crear vacío **GeometryCollection** instancia.  
  
 Un búfer negativo quita todos los puntos dentro de la distancia especificada del límite de la **geometry** instancia.  
  
 El error entre el búfer teórico y calculada es max (tolerancia a errores, extensiones \* 1.E-7) donde la tolerancia es el valor de la *tolerancia* parámetro. Para obtener más información sobre extensiones, consulte [referencia de método de tipo de datos geometry](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` y se usa `BufferWithTolerance()` para obtener un búfer aproximado a su alrededor.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [STBuffer &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

