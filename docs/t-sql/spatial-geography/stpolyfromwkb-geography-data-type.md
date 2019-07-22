---
title: STPolyFromWKB (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPolyFromWKB_TSQL
- STPolyFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPolyFromWKB method
ms.assetid: d236e0ea-dabe-4341-a6eb-ecc210d1f056
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 68ce1a309d3b6abf77e2fe9d3f571f9c4f738cef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120799"
---
# <a name="stpolyfromwkb-geography-data-type"></a>STPolyFromWKB (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una instancia de **geographyPolygon** a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC).
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STPolyFromWKB ( 'WKB_polygon' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_polygon*  
 Es la representación WKB de la instancia de **geographyPolygon** que se quiere devolver. *WKB_polygon* es una expresión **varbinary(max)** .  
  
 *SRID*  
 Es una expresión de tipo **int** que representa el identificador de referencia espacial (SRID) de la instancia **geographyPolygon** que se quiere devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
 Tipo de OGC: **Polígono**  
  
## <a name="remarks"></a>Notas  
 Este método produce una excepción **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STPolyFromWKB()` para crear una instancia de `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::STPolyFromWKB(0x01030000000100000005000000F4FDD478E9965EC0DD24068195D3474083C0CAA145965EC0508D976E12D3474083C0CAA145965EC04E62105839D44740F4FDD478E9965EC04E62105839D44740F4FDD478E9965EC0DD24068195D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de geografía estáticos de OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
