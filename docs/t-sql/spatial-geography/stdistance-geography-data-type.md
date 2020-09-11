---
description: STDistance (tipo de datos geography)
title: STDistance (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a20279a70d2e68e1cb4b34eb36ffe7de633518a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417001"
---
# <a name="stdistance-geography-data-type"></a>STDistance (tipo de datos geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve la distancia más corta entre un punto de una instancia de **geography** y un punto de otra instancia de **geography**.  
  
> [!NOTE]  
>  `STDistance()` devuelve la **LineString** más corta entre dos tipos de geografía. Se aproxima mucho a la distancia geodésica. La desviación de `STDistance()` de la distancia geodésica exacta en modelos habituales de la tierra no es de más de 0,25%. Así se evita la confusión sobre las sutiles diferencias entre longitud y distancia en tipos geodésicos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STDistance ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geography*  
 Es otra instancia de **geography** a partir de la que medir la distancia entre la instancia en la que se invoca a STDistance(). Si *other_geography* está vacío, STDistance() devuelve null.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de valor devuelto de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentarios  
 El resultado se expresa en la unidad de medida definida por el [identificador de referencia espacial &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md) de datos espaciales.
STDistance() siempre devuelve *null* si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geography**.  
  
> [!NOTE]  
>  Los métodos del tipo de datos **geography** que calculan un área o distancia tendrán resultados diferentes en función del SRID de la instancia usada en el método. Para más información sobre los SRID, vea [Identificadores de referencia espacial &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se busca la distancia entre dos instancias de **geography**.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de Geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
