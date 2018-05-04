---
title: decimal y numeric (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 629e74bfffef65546c15ea6aa4c3404bbdafa972
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="decimal-and-numeric-transact-sql"></a>decimal y numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos numéricos que tienen precisión y escala fijas. Los tipos decimal y numeric son sinónimos y se pueden usar indistintamente.
  
## <a name="arguments"></a>Argumentos  
**decimal**[ **(***p*[ **,***s*] **)**] y **numeric**[ **(***p*[ **,***s*] **)**]  
Números de precisión y escala fijas. Cuando se utiliza la precisión máxima, los valores válidos se sitúan entre - 10^38 +1 y 10^38 - 1. Los sinónimos ISO para **decimal** son **dec** y **dec(***p*, *s***)**. **numeric** equivale desde el punto de vista funcional a **decimal**.
  
p (precisión)  
El número total máximo de dígitos decimales que almacenará, tanto a la izquierda como a la derecha del separador decimal. La precisión debe ser un valor comprendido entre 1 y la precisión máxima de 38. La precisión predeterminada es 18.
  
> [!NOTE]  
>  Informatica solo admite 16 dígitos significativos, sin tener en cuenta la precisión y la escala especificada.  
  
*s* (escala)  
El número de dígitos decimales que se almacenará a la derecha del separador decimal. Este número se extrae de *p* para determinar el número máximo de dígitos a la izquierda del separador decimal. El número máximo de dígitos decimales que se puede almacenar a la derecha del separador decimal. La escala debe ser un valor comprendido entre 0 y *p*. Solo es posible especificar la escala si se ha especificado la precisión. La escala predeterminada es 0; por tanto, 0 <= *s* \<= *p*. Los tamaños de almacenamiento máximo varían según la precisión.
  
|Precisión|Bytes de almacenamiento|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica (conectado a través del conector PDW de SQL Server de Informatica) solo admite 16 dígitos significativos, sin tener en cuenta la precisión y la escala especificada.  
  
## <a name="converting-decimal-and-numeric-data"></a>Convertir datos decimal y numeric
En el caso de los tipos de datos **decimal** y **numeric**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera cada combinación específica de precisión y escala como un tipo de datos distinto. Por ejemplo, **decimal(5,5)** y **decimal(5,0)** se consideran tipos de datos diferentes.
  
En las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], una constante con un separador decimal se convierte automáticamente a un valor de datos **numeric**, con la precisión y escala mínimas necesarias. Por ejemplo, la constante 12.345 se convierte a un valor **numeric** con una precisión de 5 y una escala de 3.
  
Al convertir de **decimal** o **numeric** a **float** o **real** se puede provocar una pérdida de precisión. Al convertir de **int**, **smallint**, **tinyint**, **float**, **real**, **money**  o **smallmoney** a **decimal** o **numeric** se puede provocar un desbordamiento.
  
De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa el redondeo cuando convierte un número a un valor **decimal** o **numeric** con una precisión y una escala inferiores. Sin embargo, si la opción SET ARITHABORT está establecida en ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un error cuando se produce un desbordamiento. La pérdida de precisión y escala no es suficiente para generar un error.
  
Cuando se conviertan valores float o reales a valores decimales o numéricos, el valor decimal nunca tendrá más de 17 decimales. Los valores float < 5E-18 se convertirán siempre en 0.
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se crea una tabla con los tipos de datos **decimal** y **numeric**.  Se insertan valores en cada columna y los resultados se devuelven con una instrucción SELECT.
  
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
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
