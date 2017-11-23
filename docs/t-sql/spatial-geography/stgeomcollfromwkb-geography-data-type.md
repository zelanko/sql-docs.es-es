---
title: STGeomCollFromWKB (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 07/30/2017
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
- STGeomCollFromWKB (geography Data Type)
- STGeomCollFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STMGeomCollFromWKB method
ms.assetid: bbed028c-9cd6-4236-b5e5-8e914a21f2e4
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4551839c69157e7ba1d5d24232661c9901f54aa6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="stgeomcollfromwkb-geography-data-type"></a>STGeomCollFromWKB (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un **GeometryCollection**instancia a partir de una representación Open Geospatial Consortium (OGC) Well-Known Binary (WKB).
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STGeomCollFromWKB ( 'WKB_geometrycollection' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_geometrycollection*  
 Es la representación WKB de la **GeometryCollection** instancia que se va a devolver. *WKB_geometrycollection* es un **varbinary (max)** expresión.  
  
 *SRID*  
 Es un **int** expresión que representa el espaciales identificador de referencia (SRID) de la **GeometryCollection** instancia que se va a devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 El tipo OGC de la **geography** instancia devuelta por STGeomCollFromWKB() se establece en **GeometryCollection**, **MultiPolygon**, **MultiLineString**, o **MultiPoint**, en función de la entrada WKB correspondiente.  
  
 Este método produce una **FormatException** excepción si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STGeomCollFromWKB()` para crear una instancia de `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomCollFromWKB(0x01070000000200000001010000007593180456965EC017D9CEF753D34740010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de geografía estáticos de OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
