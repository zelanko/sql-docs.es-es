---
description: STOverlaps (tipo de datos geography)
title: STOverlaps (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STOverlaps method (geography)
ms.assetid: 2babbb9c-59ef-4494-9e6b-528cf296cbd7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0a4df3ac3d6ac6b3c4d8cf212d83cc0f71582b86
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459036"
---
# <a name="stoverlaps-geography-data-type"></a>STOverlaps (tipo de datos geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve 1 si una instancia de **geography** se superpone espacialmente a otra instancia de **geography**, o 0 en caso contrario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STOverlaps ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geography*  
 Es otra instancia de **geography** con la que se compara la instancia en la que se invoca `STOverlaps()`.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentarios  
 Este método siempre devuelve null si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geography**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se usa `STOverlaps()` para ver si se superponen dos instancias de **geography**.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('POLYGON ((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
SET @h = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523), CIRCULARSTRING (-119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SELECT @g.STOverlaps(@h);  
```  
  
  
