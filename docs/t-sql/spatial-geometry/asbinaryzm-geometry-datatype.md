---
title: AsBinaryZM (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- AsBinaryZM geometry
ms.assetid: 5eae2872-adca-4b8f-8b04-4ee91ced98f1
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2b778d41e6a3d4f7701140584fd3c833a726948
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="asbinaryzm-geometry-datatype"></a>AsBinaryZM (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve la representación de Open Geospatial Consortium (OGC) Well-Known Binary (WKB) de un **geometry** instancia ampliada con los **Z** (elevación) y **M** (medida) valores pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **varbinary (max)**  
  
 Tipo de valor devuelto de CLR: **SqlBytes**  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="examples"></a>Ejemplos  
  
```tsql  
DECLARE @g1 GEOMETRY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  


