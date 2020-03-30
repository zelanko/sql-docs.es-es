---
title: AsTextZM (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsTextZM_TSQL
- AsTextZM
- AsTextZM (geometry Data Type)
- AsTextZM_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM (geometry Data Type)
ms.assetid: 08ac8aa0-aff7-4b22-87e0-1a1d55dcbc04
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 437859afd1f21cba5c47f93c86173d71e3ae89d9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68027641"
---
# <a name="astextzm-geometry-data-type"></a>AsTextZM (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de geometría ampliada con los valores **Z** (elevación) y **M** (medida) pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de valor devuelto de CLR: **SqlChars**  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` que contiene valores **Z** (elevación) y **M** (medida). `STAsText()` selecciona los valores WKT (1 2); `AsTextZM()` selecciona los mismos valores WKT y, asimismo, devuelve los valores de **Z** y **M**, lo que da como resultado (1 2 3 4).  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

