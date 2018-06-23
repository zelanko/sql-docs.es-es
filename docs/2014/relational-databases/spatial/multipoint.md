---
title: MultiPoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0106449b66e1f4c55edd28abfd4e2fab67626080
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200323"
---
# <a name="multipoint"></a>MultiPoint
  A `MultiPoint` es una colección de cero o más puntos. El límite de una instancia de `MultiPoint` está vacío.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente crea una instancia de `geometry MultiPoint` con SRID 23 y dos puntos: un punto con las coordenadas (2, 3), un punto con las coordenadas (7, 8) y un valor de Z de 9,5.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 Esta instancia de `MultiPoint` también se puede expresar usando `STMPointFromText()` como se muestra a continuación.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 El ejemplo siguiente usa el método `STGeometryN()` para recuperar una descripción del primer punto de la colección.  
  
```  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>Vea también  
 [Punto](point.md)   
 [Datos espaciales &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  