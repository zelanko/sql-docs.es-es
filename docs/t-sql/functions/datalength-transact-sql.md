---
title: DATALENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
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
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4d6baea43ef2432ce9d5c54ea15441ca014cee41
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823888"
---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función devuelve el número de bytes usados para representar cualquier expresión.

> [!NOTE]
> Para devolver el número de caracteres de una expresión de cadena, utilice la función [LEN](../../t-sql/functions/len-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>Argumentos  
*expression*  
Una [expression](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de datos.
  
## <a name="return-types"></a>Tipos de valores devueltos
**bigint** si *expression* tiene el tipo de datos **nvarchar(max)** , **varbinary(max)** o **varchar(max)** ; en caso contrario, **int**.
  
## <a name="remarks"></a>Observaciones  
`DATALENGTH` resulta muy útil cuando se usa con tipos de datos que pueden almacenar datos de longitud variable, como:
- **image**
- **ntext**
- **nvarchar**
- **text**
- **varbinary**
- **varchar**
  
Para un valor NULL, `DATALENGTH` devuelve NULL.
  
> [!NOTE]  
> Los niveles de compatibilidad pueden afectar a los valores devueltos. Vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) para más información sobre los niveles de compatibilidad.  

> [!NOTE]
> Use [LEN](../../t-sql/functions/len-transact-sql.md) para devolver el número de caracteres codificados en una expresión de cadena determinada y [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) para devolver el tamaño en bytes para una expresión de cadena determinada. Estos resultados pueden diferir en función del tipo de datos y del tipo de codificación utilizado en la columna. Para obtener más información sobre las diferencias de almacenamiento entre los distintos tipos de codificación, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).

## <a name="examples"></a>Ejemplos  
En este ejemplo se busca la longitud de la columna `Name` en la tabla `Product`:
  
```sql
USE AdventureWorks2016  
GO
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>Consulte también
[LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)
