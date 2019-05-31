---
title: Long (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 2287205c91f2ceaef44af7bf8322d3c31e201c0c
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937659"
---
# <a name="long-geography-data-type"></a>Long (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Propiedad de longitud de la instancia de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 En el modelo OpenGIS, Long se define solo en instancias de **geography** que constan de un solo punto. Esta propiedad devuelve NULL si las instancias de **geography** contienen más de un punto. Esta propiedad es precisa y de solo lectura.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se crea una instancia de **Point** y se recupera la longitud del punto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
