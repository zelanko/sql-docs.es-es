---
description: Prioridad de tipo de datos (Transact-SQL)
title: Prioridad de tipo de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6ed8d2a30d4bcc2cd1adaedc3cccd6642d701533
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459936"
---
# <a name="data-type-precedence-transact-sql"></a>Prioridad de tipo de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md.md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Cuando un operador combina dos expresiones de tipos de datos distintos, el tipo de datos con la prioridad más baja se convierte primero al tipo de datos con la prioridad más alta. Si la conversión no es una conversión implícita admitida, se devuelve un error. Para un operador que combina expresiones de operandos que tienen el mismo tipo de datos, el resultado de la operación tiene ese tipo de datos.
  
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
  
