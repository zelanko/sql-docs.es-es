---
title: DATALENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5f1b4816be53f05dd964f8be0ee9ce52fd11cbb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65943787"
---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función devuelve el número de bytes usados para representar cualquier expresión.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>Argumentos  
*expression*  
Una [expression](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de datos.
  
## <a name="return-types"></a>Tipos de valores devueltos
**bigint** si *expression* tiene el tipo de datos **nvarchar(max)** , **varbinary(max)** o **varchar(max)** ; en caso contrario, **int**.
  
## <a name="remarks"></a>Notas  
`DATALENGTH` es muy útil cuando se usa con tipos de datos

- **imagen**
- **ntext**
- **nvarchar**
- **texto**
- **varbinary**
- **varchar**

porque estos tipos de datos pueden almacenar datos de longitud variable.
  
Para un valor NULL, `DATALENGTH` devuelve NULL.
  
> [!NOTE]  
>  Los niveles de compatibilidad pueden afectar a los valores devueltos. Vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) para más información sobre los niveles de compatibilidad.  
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se busca la longitud de la columna `Name` en la tabla `Product`:
  
```sql
-- Uses AdventureWorks  
  
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>Vea también
[LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  

