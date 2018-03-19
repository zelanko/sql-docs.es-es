---
title: STMLineFromWKB (tipo de datos geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
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
- STMLineFromWKB_TSQL
- STMLineFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STMLineFromWKB method
ms.assetid: 05ca6d65-4799-4b9a-9672-cfebae95f23e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3130c8b4b20e4d3c1cd65637693ef0c141cb3f9f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="stmlinefromwkb-geography-data-type"></a>STMLineFromWKB (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una instancia de **geographyMultiLineString** a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC).
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STMLineFromWKB ( 'WKB_multilinestring' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_multilinestring*  
 Es la representación WKB de la instancia de **geographyMultiLineString** que se va a devolver. *WKB_multilinestring* es una expresión **varbinary(max)**.  
  
 *SRID*  
 Es una expresión **int** que representa el identificador de referencia espacial (SRID) de la instancia de **geographyMultiLineString** que se quiere devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
 Tipo OGC: **MultiLineString**  
  
## <a name="remarks"></a>Notas  
 Este método produce una excepción **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STMLineFromWKB()` para crear un instancia de `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STMLineFromWKB(0x010500000002000000010200000005000000F4FDD478E9965EC0DD24068195D3474083C0CAA145965EC0508D976E12D3474083C0CAA145965EC04E62105839D44740F4FDD478E9965EC04E62105839D44740F4FDD478E9965EC0DD24068195D34740010200000005000000022B8716D9965EC0C1CAA145B6D34740022B8716D9965EC06ABC749318D447407593180456965EC06ABC749318D447407593180456965EC03333333333D34740022B8716D9965EC0C1CAA145B6D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de geografía estáticos de OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
