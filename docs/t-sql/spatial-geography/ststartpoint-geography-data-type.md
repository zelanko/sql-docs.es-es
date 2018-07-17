---
title: STStartPoint (tipo de datos geography) | Microsoft Docs
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
- STStartPoint_TSQL
- STStartPoint (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STStartPoint method
ms.assetid: 7df18a5f-b9ee-4e36-b765-a0790c1dee3d
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b46b802656930cbd5d1f77f0e088bf7f4a696d2d
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36256857"
---
# <a name="ststartpoint-geography-data-type"></a>STStartPoint (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el punto inicial de una instancia de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STStartPoint ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
 Tipo Open Geospatial Consortium (OGC): **Point**  
  
## <a name="remarks"></a>Notas  
 STStartPoint() es el equivalente de [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)`(1)`.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` y se utiliza `STStartPoint()` para recuperar el punto de inicio de la instancia.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STStartPoint().ToString();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
