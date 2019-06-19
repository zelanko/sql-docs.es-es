---
title: AsTextZM (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 8b4d5e834faa455eeb62e67f396447d44a176f55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65936378"
---
# <a name="astextzm-geography-data-type"></a>AsTextZM (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de **geography** ampliada con los valores **Z** (elevación) y **M** (medida) pertenecientes a la instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de valor devuelto de CLR: **SqlChars**  
  
## <a name="remarks"></a>Notas  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` que contiene valores **Z** (elevación) y **M** (medida). `STAsText()` selecciona los valores WKT (-122.34900 47.65100); `AsTextZM()` selecciona los mismos valores WKT y también devuelve los valores para **Z** y **M**, lo que da como resultado (-122.34900 47.65100 10.3 12).  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
