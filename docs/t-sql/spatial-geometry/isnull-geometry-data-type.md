---
title: IsNull (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: IsNull (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 25b4699265ec8cc5f2db2ef7cbfb8bb9813c3626
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="isnull-geometry-data-type"></a>IsNull (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

El tipo de un **geometry** instancia es null. Devuelve 0 si la instancia no es NULL.
  
## <a name="syntax"></a>Sintaxis  
  
```  
.IsNull  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **bits**  
  
 Tipo CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentarios  
 `IsNull`puede utilizarse para probar si una **geometry** instancia es null. Esto puede producir resultados un tanto confusos, devolviendo 0 si la instancia no es NULL y NULL si la instancia es NULL.  
  
 Este método lo usa principalmente la infraestructura de SQL Server; no es recomendable usar `IsNull` para comprobar si una instancia es NULL.  
  

## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

