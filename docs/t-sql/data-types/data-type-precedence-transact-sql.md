---
title: Tipo de datos de prioridad (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/23/2017
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
- precedence [SQL Server]
- data types [SQL Server], converting
- data types [SQL Server], precedence
- converting data types [SQL Server], precedence
- precedence [SQL Server], data types
ms.assetid: f4c804ab-ed3f-43b1-a024-c9ac6944b66b
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f39337e00dfdbcd4a6bb01a00093a61f46a79fa
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-precedence-transact-sql"></a>Precedencia de tipo de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Cuando un operador combina dos expresiones de tipos de datos distintos, las reglas de prioridad de tipo de datos especifican que el tipo de datos con la prioridad más baja se convierta al tipo de datos con la prioridad más alta. Si la conversión no es una conversión implícita admitida, se devuelve un error. Cuando ambas expresiones de operandos tienen el mismo tipo de datos, el resultado de la operación tiene ese tipo de datos.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el siguiente orden de prioridad para los tipos de datos:
  
1.  tipos de datos definidos por el usuario (el más alto)  
1.  **sql_variant**  
1.  **xml**  
1.  **datetimeoffset**  
1.  **datetime2**  
1.  **datetime**  
1.  **smalldatetime**  
1.  **date**  
1. **time**  
1. **float**  
1. **real**  
1. **decimal**  
1. **money**  
1. **smallmoney**  
1. **bigint**  
1. **int**  
1. **smallint**  
1. **tinyint**  
1. **bit**  
1. **ntext**  
1. **text**  
1. **image**  
1. **timestamp**  
1. **uniqueidentifier**  
1. **nvarchar** (incluidos **nvarchar (max)** )  
1. **nchar**  
1. **varchar** (incluidos **varchar (max)** )  
1. **char**  
1. **varbinary** (incluidos **varbinary (max)** )  
1. **binario** (el más bajo)  
  
## <a name="see-also"></a>Vea también
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

