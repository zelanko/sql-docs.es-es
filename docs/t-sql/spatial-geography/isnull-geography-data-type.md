---
description: IsNull (tipo de datos geography)
title: IsNull (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: cd161c4d14241a6596e2a54ae79cd919fb776c59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422379"
---
# <a name="isnull-geography-data-type"></a>IsNull (tipo de datos geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Propiedad que especifica si la instancia de **geography** es NULL. Devuelve 'TRUE' si la instancia es NULL; en caso contrario, devuelve 0.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.IsNull  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de valor devuelto
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Observaciones  
 `IsNull` se puede usar para comprobar si una instancia de **geography** es NULL. Esto puede producir resultados un tanto confusos, devolviendo 0 si la instancia no es NULL y NULL si la instancia es NULL.  
  
 Este método lo usa principalmente la infraestructura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; se recomienda usar el predicado IS NULL de T-SQL para comprobar si una instancia de **geography** es NULL. Para más información sobre el predicado IS NULL de T-SQL, vea [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
