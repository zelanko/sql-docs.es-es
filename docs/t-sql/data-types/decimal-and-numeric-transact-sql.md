---
title: decimal y numeric (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6c8ec4ea2255e8496b6e5ed464fbff220d270e7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="decimal-and-numeric-transact-sql"></a>decimal y numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos numéricos que tienen precisión y escala fijas. Decimal y numeric son sinónimos y se pueden usar indistintamente.
  
## <a name="arguments"></a>Argumentos  
**decimal**[ **(***p*[ **,***s*] **)**] y **numérico** [ **(***p*[ **,***s*] **)**]  
Números de precisión y escala fijas. Cuando se utiliza la precisión máxima, los valores válidos se sitúan entre - 10^38 +1 y 10^38 - 1. Los sinónimos ISO de **decimal** son **dec** y **dec (***p*, *s***)**. **numérico** es funcionalmente equivalente a **decimal**.
  
p (precisión)  
El número total máximo de dígitos decimales que almacenará, tanto a la izquierda como a la derecha del separador decimal. La precisión debe ser un valor comprendido entre 1 y la precisión máxima de 38. La precisión predeterminada es 18.
  
> [!NOTE]  
>  Informatica solo admite 16 dígitos significativos, sin tener en cuenta la precisión y la escala especificada.  
  
*s* (escala)  
El número de dígitos decimales que se almacenará a la derecha del separador decimal. Este número se resta de *p* para determinar el número máximo de dígitos a la izquierda del separador decimal. El número máximo de dígitos decimales que se puede almacenar a la derecha del separador decimal. Escala debe ser un valor comprendido entre 0 y *p*. Solo es posible especificar la escala si se ha especificado la precisión. La escala predeterminada es 0; por lo tanto, 0 < = *s* \< =  *p*. Los tamaños de almacenamiento máximo varían según la precisión.
  
|Precisión|Bytes de almacenamiento|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica (conectado a través del conector de SQL Server PDW Informatica) sólo admite 16 dígitos significativos, sin tener en cuenta la precisión y la escala especificada.  
  
## <a name="converting-decimal-and-numeric-data"></a>Convertir datos decimal y numeric
Para el **decimal** y **numérico** tipos de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera cada combinación específica de precisión y escala como un tipo de datos diferente. Por ejemplo, **decimal(5,5)** y **decimal(5,0)** se consideran tipos de datos diferentes.
  
En [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones, una constante con un separador decimal se convierte automáticamente en un **numérico** datos de valor, con la precisión mínima y escalar necesarios. Por ejemplo, la constante 12.345 se convierte en una **numérico** valor con una precisión de 5 y una escala de 3.
  
Convertir de **decimal** o **numérico** a **float** o **real** puede provocar una pérdida de precisión. Convertir de **int**, **smallint**, **tinyint**, **float**, **real**, **money** , o **smallmoney** como **decimal** o **numérico** puede ocasionar el desbordamiento.
  
De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa el redondeo cuando convierte un número a un **decimal** o **numérico** valor con una precisión y escala inferiores. Sin embargo, si la opción SET ARITHABORT está establecida en ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un error cuando se produce un desbordamiento. La pérdida de precisión y escala no es suficiente para generar un error.
  
Cuando se conviertan valores float o reales a valores decimales o numéricos, el valor decimal nunca tendrá más de 17 decimales. Los valores float < 5E-18 se convertirán siempre en 0.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se crea una tabla con el **decimal** y **numérico** tipos de datos.  Se insertan valores en cada columna y los resultados se devuelven con una instrucción SELECT.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn decimal(5,2)  
,MyNumericColumn numeric(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Vea también
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sys.Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

