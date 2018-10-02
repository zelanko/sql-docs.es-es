---
title: '- (Negativo) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- negative
dev_langs:
- TSQL
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
- negative values
ms.assetid: d6c14d14-d379-403b-82db-c197ad58c896
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4819d10eb31e42b31a87483f741802aa8a290bba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678073"
---
# <a name="unary-operators---negative"></a>Operadores unarios: negativo
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el valor negativo de una expresión numérica (un operador unario). Los operadores unarios realizan una operación sobre una única expresión de cualquiera de los tipos de datos de la categoría del tipo de datos numérico.   
  
|Operador|Significado|  
|--------------|-------------|  
|[+ (Positivo)](../../t-sql/language-elements/unary-operators-positive.md)|El valor numérico es positivo.|  
|[- (Negativo)](../../t-sql/language-elements/unary-operators-negative.md)|El valor numérico es negativo.|  
|[~ (NOT bit a bit)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|Devuelve los bits complementarios del número.|  
  
 Los operadores + (Positivo) y - (Negativo) se pueden utilizar en cualquier expresión de cualquiera de los tipos de datos de la categoría del tipo de datos numérico. El operador ~ (NOT bit a bit) solo se puede utilizar en expresiones de cualquiera de los tipos de datos de la categoría del tipo de datos entero. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
- numeric_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Es cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) válida de cualquiera de los tipos de datos de la categoría del tipo de datos numérico, a excepción de la categoría de fecha y hora.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos de *expresión_numérica*, excepto si se trata de una expresión **tinyint** sin signo que se promueve a un resultado **smallint** con signo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-setting-a-variable-to-a-negative-value"></a>A. Establecer una variable con un valor negativo  
 En el ejemplo siguiente se establece una variable con un valor negativo.  
  
```  
USE tempdb;  
GO  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = -123.45;  
SELECT @MyNumber AS NegativeValue;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
NegativeValue  
---------------------------------------  
-123.45  
  
(1 row(s) affected)  
  
```  
  
### <a name="b-changing-a-variable-to-a-negative-value"></a>B. Cambiar una variable a un valor negativo  
 En el ejemplo siguiente se cambia una variable a un valor negativo.  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = 5;  
SELECT @Num1 AS VariableValue, -@Num1 AS NegativeValue;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
VariableValue NegativeValue  
------------- -------------  
5             -5  
  
(1 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-negative-of-a-positive-constant"></a>C. Devolución del valor negativo de una constante positiva  
 En el ejemplo siguiente se devuelve el valor negativo de una constante positiva.  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) - 17 FROM DimEmployee;  
```  
  
 Devuelve  
  
```  
-17  
```  
  
### <a name="d-returning-the-positive-of-a-negative-constant"></a>D. Devolución del valor positivo de una constante negativa  
 En el ejemplo siguiente se devuelve el valor positivo de una constante negativa.  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) – ( - 17) FROM DimEmployee;  
```  
  
 Devuelve  
  
```  
17  
```  
  
### <a name="e-returning-the-negative-of-a-column"></a>E. Devolución del valor negativo de una columna  
 En el ejemplo siguiente se devuelve el valor negativo del valor `BaseRate` de cada empleado de la tabla `dimEmployee`.  
  
```  
USE ssawPDW;  
  
SELECT - BaseRate FROM DimEmployee;  
```  
  
## <a name="see-also"></a>Ver también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  

