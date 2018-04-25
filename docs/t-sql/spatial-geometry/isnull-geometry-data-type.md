---
title: IsNull (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IsNull (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f9b97eaa73b70beea9e56b2e4a07e99ea9e9e83
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="isnull-geometry-data-type"></a>IsNull (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

El tipo de una instancia de **geometry** es NULL. Devuelve 0 si la instancia no es NULL.
  
## <a name="syntax"></a>Sintaxis  
  
```  
.IsNull  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Notas  
 `IsNull` se puede usar para comprobar si una instancia de **geometry** es NULL. Esto puede producir resultados un tanto confusos, devolviendo 0 si la instancia no es NULL y NULL si la instancia es NULL.  
  
 Este método lo usa principalmente la infraestructura de SQL Server; no es recomendable usar `IsNull` para comprobar si una instancia es NULL.  
  

## <a name="see-also"></a>Ver también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

