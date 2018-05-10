---
title: STLineFromWKB (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STLineFromWKB (geography Data Type)
- STLineFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromWKB method
ms.assetid: 8ac2b772-6673-4ba1-a7ab-3b4b5841560b
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f776ef8ba0ead4c9f1dabcc37ef431fe4e16588b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="stlinefromwkb-geography-data-type"></a>STLineFromWKB (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una instancia de **LineString geography** a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC).
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STLineFromWKB ( 'WKB_linestring' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_linestring*  
 Es la representación WKB de la instancia de **LineString geography** que se quiere devolver. *WKB_linestring* es una expresión **varbinary(max)**.  
  
 *SRID*  
 Es una expresión **int** que representa el identificador de referencia espacial (SRID) de la instancia **LineString geography** que se quiere devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
 Tipo OGC: **LineString**  
  
## <a name="remarks"></a>Notas  
 Este método produce una excepción **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STLineFromWKB()` para crear un instancia de `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STLineFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de geografía estáticos de OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
