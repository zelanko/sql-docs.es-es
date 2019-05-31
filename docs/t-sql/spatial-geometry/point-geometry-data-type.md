---
title: Point (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
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
- Point (geometry Data Type)
ms.assetid: 7a2e593a-4d4c-4214-b0c5-02d1ac46bc66
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 2d4ddfdf1721b31ddced529682c8a619f8673644
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937443"
---
# <a name="point-geometry-data-type"></a>Point (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Construye una instancia de **geometry** que representa una instancia de **Point** a partir de sus valores X e Y, y de un SRID.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Point ( X, Y, SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *X*  
 Es una expresión **float** que representa la coordenada X del elemento **Point** que se está generando.  
  
 *S*  
 Es una expresión **float** que representa la coordenada Y del elemento **Point** que se está generando.  
  
 *SRID*  
 Es una expresión **int** que representa el identificador de referencia espacial (SRID) de la instancia de **geometry** que se quiere devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Notas  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `Point()` para crear una instancia de `geometry`.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Point(1, 10, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de geometría estáticos ampliados](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

