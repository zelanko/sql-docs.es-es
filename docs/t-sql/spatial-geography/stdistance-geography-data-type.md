---
title: STDistance (tipo de datos geography) | Microsoft Docs
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
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3d4fef2b2ba45c8d7fe36becf5893d798c87c536
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36255267"
---
# <a name="stdistance-geography-data-type"></a>STDistance (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve la distancia más corta entre un punto de una instancia de **geography** y un punto de otra instancia de **geography**.  
  
> [!NOTE]  
>  `STDistance()` devuelve la **LineString** más corta entre dos tipos de geografía. Se aproxima mucho a la distancia geodésica. La desviación de `STDistance()` de la distancia geodésica exacta en modelos habituales de la tierra no es de más de 0,25%. Así se evita la confusión sobre las sutiles diferencias entre longitud y distancia en tipos geodésicos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STDistance ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 Es otra instancia de **geography** a partir de la que medir la distancia entre la instancia en la que se invoca a STDistance(). Si *other_geography* está vacío, STDistance() devuelve null.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de valor devuelto de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 STDistance() siempre devuelve null si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geography**.  
  
> [!NOTE]  
>  Los métodos del tipo de datos **geography** que calculan un área o distancia tendrán resultados diferentes en función del SRID de la instancia usada en el método.   Para más información sobre los SRID, vea [Identificadores de referencia espacial &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se busca la distancia entre dos instancias de **geography**.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
