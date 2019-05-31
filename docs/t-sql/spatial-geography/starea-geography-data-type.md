---
title: STArea (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 49919caaf30bb425e90b286cb3c8e7877067ae6d
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936242"
---
# <a name="starea-geography-data-type"></a>STArea (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el área expuesta total de una instancia de **geography**. Los resultados para STArea() son la unidad al cuadrado de la medida que el identificador de referencia espacial de la instancia de **geography** usa. Por ejemplo, si el SRID de la instancia es 4326, STArea() devuelve resultados en metros cuadrados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
Tipo de valor devuelto de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
STArea() devuelve cero si una instancia de **geography** contiene únicamente figuras no dimensionales o unidimensionales, o si está vacía.  
  
> [!NOTE]  
>  Los métodos del tipo de datos **geography** que generan un valor devuelto métrico tendrán resultados diferentes en función del SRID de la instancia usada en el método. Para más información sobre los SRID, vea [Identificadores de referencia espacial &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se usa `STArea()` para crear una instancia de `Polygon geography` y se calcula el área del polígono.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>Consulte también  
[Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
