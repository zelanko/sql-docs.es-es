---
title: Prioridad de tipo de datos (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e61ec1dec12552219279370f01fe0dd494a22cbe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="data-type-precedence-transact-sql"></a>Prioridad de tipo de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
1. **texto**  
1. **imagen**  
1. **timestamp**  
1. **uniqueidentifier**  
1. **nvarchar** (**nvarchar(max)** incluido)  
1. **nchar**  
1. **varchar** (**varchar(max)** incluido)  
1. **char**  
1. **varbinary** (**varbinary(max)** incluido)  
1. **binary** (el más bajo)  
  
## <a name="see-also"></a>Vea también
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
