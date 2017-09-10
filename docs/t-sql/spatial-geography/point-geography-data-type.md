---
title: Punto (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cefb6e199bbd4617b1fc2f6f71d9bb3997445dc
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="point-geography-data-type"></a>Point (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Construye un **geography** instancia que representa un **punto** instancia a partir de sus valores de latitud y longitud y una referencia espacial (SRID) de identificador.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *LAT*  
 Es un **float** expresión que representa la coordenada x de la **punto** que se está generando.  
  
 *Long*  
 Es un **float** expresión que representa la coordenada y de la **punto** que se está generando. Para obtener más información sobre los valores de longitud y latitud válida, consulte [punto](../../relational-databases/spatial/point.md).  
  
 *SRID*  
 Es un **int** expresión que representa el SRID de la **geography** instancia que se va a devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
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
  
## <a name="see-also"></a>Vea también  
 [Métodos de geografía estáticos extendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

