---
title: STPointN (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: f7bbaf25715275b14deda0f2a510b40934c6f33e
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938383"
---
# <a name="stpointn-geometry-data-type"></a>STPointN (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un punto especificado de una instancia de **geometry**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es una expresión **int** entre 1 y el número de puntos de la instancia de **geometry**.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
 Tipo Open Geospatial Consortium (OGC): **Point**  
  
## <a name="remarks"></a>Notas  
 Si se trata de una instancia de **geometry** creada por el usuario, `STPointN()` devuelve el punto especificado por *expression* considerando los puntos en el orden en el que se especificaron inicialmente.  
  
 Si se trata de una instancia de **geometry** generada por el sistema, `STPointN()` devuelve el punto especificado por *expression* considerando todos los puntos en el orden en que se generarían: primero por geometrías, después por anillos dentro de la geometría (si procede) y, luego, por puntos dentro del anillo. Este orden es determinista.  
  
 Si se llama a este método con un valor inferior a 1, se genera una excepción **ArgumentOutOfRangeException**.  
  
 Si se llama a este método con un valor superior al número de puntos de la instancia, devuelve NULL.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` y se usa `STPointN()` para recuperar el segundo punto de la descripción de la instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

