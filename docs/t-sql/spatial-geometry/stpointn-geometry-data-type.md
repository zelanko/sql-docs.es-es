---
title: STPointN (tipo de datos geometry) | Documentos de Microsoft
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
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb3933aee8f8880b23bb4883753acb85d83ddb1e
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="stpointn-geometry-data-type"></a>STPointN (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un punto especificado en un **geometry** instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es un **int** expresión entre 1 y el número de puntos en el **geometry** instancia.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
 Abrir tipo Geospatial Consortium (OGC): **punto**  
  
## <a name="remarks"></a>Comentarios  
 Si un **geometry** instancia es usuario creado, `STPointN()` devuelve el punto especificado por *expresión* Considerando los puntos en el orden en el que se especificaron inicialmente.  
  
 Si un **geometry** instancia generada por el sistema, `STPointN()` devuelve el punto especificado por *expresión* considerando todos los puntos en el mismo orden que serían salida: primero por geometrías, a continuación, por anillos dentro de la geometría (si procede) y, a continuación, según el punto en el anillo. Este orden es determinista.  
  
 Si se llama a este método con un valor menor que 1, produce un **ArgumentOutOfRangeException**.  
  
 Si se llama a este método con un valor superior al número de puntos de la instancia, devuelve NULL.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` y se usa `STPointN()` para recuperar el segundo punto de la descripción de la instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

