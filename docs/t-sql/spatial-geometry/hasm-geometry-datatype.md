---
title: HasM (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 05/05/2017
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
- HasM geometry
ms.assetid: 15540837-c4bf-4d18-b380-13ae31f3226f
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5086605b21d8ad5df273c67bf5737b9fb4279673
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="hasm-geometry-datatype"></a>HasM (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve 1 (true) si un objeto espacial contiene al menos un valor M; de lo contrario, devuelve 0 (false).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.HasM  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **bits**  
  
 Tipo de valor devuelto de CLR: **booleano**  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="examples"></a>Ejemplos  
  
```tsql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)  
  
  

