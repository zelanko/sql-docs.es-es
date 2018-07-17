---
title: AsTextZM (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0ed2501681a9a1b1ecb8523149706427710ed187
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36251377"
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
  
## <a name="see-also"></a>Ver también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
