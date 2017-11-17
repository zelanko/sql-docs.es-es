---
title: STPointN (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
f1_keywords:
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15a196cf9ac1c5f560a2eeee3d0262829f88480b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stpointn-geography-data-type"></a>STPointN (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el punto especificado en un **geography** instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es un **int** expresión entre 1 y el número de puntos en el **geography** instancia.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
 Abrir tipo Geospatial Consortium (OGC): **punto**  
  
## <a name="remarks"></a>Comentarios  
 Si un **geography** instancia es creada por el usuario, STPointN() devuelve el punto especificado por *expresión* Considerando los puntos en el orden en el que se especificaron inicialmente.  
  
 Si un **geography** instancia es generada por el sistema, STPointN() devuelve el punto especificado por *expresión* considerando todos los puntos en el mismo orden que serían salida: primero por  **Geography** instancia, después por anillos dentro de la instancia (si procede) y, a continuación, según el punto en el anillo. Este orden es determinista.  
  
 Si se llama a este método con un valor menor que 1, produce un **ArgumentOutOfRangeException**.  
  
 Si se llama a este método con un valor superior al número de puntos de la instancia, devuelve NULL.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` y se usa `STPointN()` para recuperar el segundo punto de la descripción de la instancia.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de Geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

