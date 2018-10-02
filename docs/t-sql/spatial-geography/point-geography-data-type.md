---
title: Point (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Point
- Point_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4de164536b75684d8c019a9f93db4a9b21415650
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759813"
---
# <a name="point-geography-data-type"></a>Point (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Construye una instancia de **geography** que representa una instancia de **Point** a partir de sus valores de latitud y longitud y de un identificador de referencia espacial (SRID).
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Lat*  
 Es una expresión **float** que representa la coordenada X del elemento **Point** que se está generando.  
  
 *Long*  
 Es una expresión **float** que representa la coordenada Y del elemento **Point** que se está generando. Para más información sobre los valores de latitud y longitud correctos, vea [Punto](../../relational-databases/spatial/point.md).  
  
 *SRID*  
 Es una expresión **int** que representa el SRID de la instancia de **geography** que se quiere devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
> [!NOTE]  
>  Los argumentos para el método de punto (tipo de datos de geografía) tienen coordenadas invertidas en comparación con WKT.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `Point()` para crear una instancia de `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de geografía estáticos extendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
