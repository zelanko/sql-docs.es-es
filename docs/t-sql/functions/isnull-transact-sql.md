---
title: ISNULL (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISNULL
- ISNULL_TSQL
- IFNULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- replacing null values
- null values [SQL Server], ISNULL
- null values [SQL Server], replacement values
- ISNULL function
ms.assetid: 6f3e5802-864b-4e77-9862-657bb5430b68
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8d364548d3303de493343365bd16677ffdfd5641
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="isnull-transact-sql"></a>ISNULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Sustituye el valor NULL por el valor especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ISNULL ( check_expression , replacement_value )  
```  
  
## <a name="arguments"></a>Argumentos  
 *check_expression*  
 Es el [expresión](../../t-sql/language-elements/expressions-transact-sql.md) para comprobar si hay valores NULL. *check_expression* puede ser de cualquier tipo.  
  
 *replacement_value*  
 Es la expresión que se devuelve si *check_expression* es NULL. *replacement_value* debe ser de un tipo que sea implícitamente convertible al tipo de *check_expresssion*.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve el mismo tipo que *check_expression*. Si se proporciona un literal NULL como *check_expression*, devuelve el tipo de datos de la *replacement_value*. Si se proporciona un literal NULL como *check_expression* y no *replacement_value* se proporciona, se devuelve un **int**.  
  
## <a name="remarks"></a>Comentarios  
 El valor de *check_expression* se devuelve si no es NULL; en caso contrario, *replacement_value* se devuelve después de que se convierte implícitamente al tipo de *check_expression*, si los tipos son diferentes. *replacement_value* se puede truncar si *replacement_value* es mayor que *check_expression*.  
  
> [!NOTE]  
>  Use [COALESCE &#40; Transact-SQL &#41; ](../../t-sql/language-elements/coalesce-transact-sql.md) para devolver el primer valor distinto de null.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-isnull-with-avg"></a>A. Usar ISNULL con AVG  
 En el ejemplo siguiente se busca el promedio del peso de todos los productos. Sustituye el valor `50` para todas las entradas NULL en la columna `Weight` de la tabla `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AVG(ISNULL(Weight, 50))  
FROM Production.Product;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------------- 
59.79  
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-isnull"></a>B. Usar ISNULL  
 En el siguiente ejemplo se selecciona la descripción, el porcentaje de descuento, la cantidad mínima y la cantidad máxima de todas las ofertas especiales de `AdventureWorks2012`. Si la cantidad máxima de una oferta especial determinada es NULL, el valor de `MaxQty` mostrado en el conjunto de resultados es `0.00`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Description, DiscountPct, MinQty, ISNULL(MaxQty, 0.00) AS 'Max Quantity'  
FROM Sales.SpecialOffer;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|  Description       |  DiscountPct    |   MinQty    |   Cantidad máxima       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0.02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0.20           |   61        |   0                  |
|  Cl Mountain-100   |  0.35           |   0         |   0                  |
|  Sport casco Di   |  0.10           |   0         |   0                  |
|  Overst Road-650   |  0.30           |   0         |   0                  |
|  Mountain Tire S   |  0.50           |   0         |   0                  |
|  Sport casco Di   |  0.15           |   0         |   0                  |
|  Bicicleta de montaña LL S   |  0.35           |   0         |   0                  |
|  Pr Touring-3000   |  0.15           |   0         |   0                  |
|  Pr Touring-1000   |  0.20           |   0         |   0                  |
|  Precio medio Peda   |  0.50           |   0         |   0                  |
|  Si Mountain-500   |  0.40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### <a name="c-testing-for-null-in-a-where-clause"></a>C. Comprobar si hay valores NULL en una cláusula WHERE  
 No utilice ISNULL para buscar los valores NULL. Use IS NULL en su lugar. En el ejemplo siguiente se buscan todos los productos que tienen `NULL` en la columna de peso. Tenga en cuenta el espacio entre `IS` y `NULL`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>D. Usar ISNULL con AVG  
 En el ejemplo siguiente se busca el promedio del peso de todos los productos en una tabla de ejemplo. Sustituye el valor `50` para todas las entradas NULL en la columna `Weight` de la tabla `Product`.  
  
```  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### <a name="e-using-isnull"></a>E. Usar ISNULL  
 En el ejemplo siguiente se usa ISNULL para comprobar los valores NULL en la columna `MinPaymentAmount` y mostrar el valor `0.00` para las filas.  
  
```  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  Una asociación de bicicleta       |     0.0000         |
|  Un almacén de bicicleta                |     0.0000         |
|  Una tienda de ciclo                |     0.0000         |
|  Una gran empresa de bicicleta     |     0.0000         |
|  Una tienda de bicicletas típico         |   200.0000         |
|  Servicio & ventas aceptables  |     0.0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. Uso de IS NULL para probar si hay valores NULL en una cláusula WHERE  
 En el ejemplo siguiente se busca todos los productos que tienen `NULL` en la `Weight` columna. Tenga en cuenta el espacio entre `IS` y `NULL`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [ES NULL &#40; Transact-SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [COALESCE &#40; Transact-SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  


