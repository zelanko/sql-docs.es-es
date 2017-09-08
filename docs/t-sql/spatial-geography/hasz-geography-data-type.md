---
title: HasZ (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HasZ
- HasZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- HasZ geography
ms.assetid: 4c5e1669-a987-4dda-9ebf-f573ce615c34
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15a39d4b7b9f4fa1a8d15562db8bc68ff24e18fb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="hasz-geography-data-type"></a>HasZ (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve 1 (true) si un objeto espacial contiene al menos un valor Z; de lo contrario, devuelve 0 (false).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.HasZ  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **bits**  
  
 Tipo de valor devuelto de CLR: **booleano**  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="examples"></a>Ejemplos  
  
```tsql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasZ   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  

