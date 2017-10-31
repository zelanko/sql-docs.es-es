---
title: Money y smallmoney (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- money_TSQL
- money
- smallmoney
- smallmoney_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- money data type, about money data type
- money data type
- smallmoney data type
- values [SQL Server], monetary
- currency [SQL Server]
ms.assetid: 57861137-89ea-4b89-b361-390597d7bccc
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bd07ecd1cdacc686e0f831320fd5e939c0c174da
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="money-and-smallmoney-transact-sql"></a>money y smallmoney (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos que representan valores monetarios o de moneda.
  
## <a name="remarks"></a>Comentarios  
  
|Tipo de datos|Intervalo|Almacenamiento|  
|---|---|---|
|**money**|-922.337.203.685.477,5808 a 922.337.203.685.477,5807 (-922,337,203,685,477.58<br />para 922,337,203,685,477.58 de Informatica.  Informatica solo es compatible con dos decimales, no cuatro.)|8 bytes|  
|**smallmoney**|De - 214.748,3648 a 214.748,3647|4 bytes|  
  
El **dinero** y **smallmoney** tipos de datos tienen una precisión de una diezmilésima de las unidades monetarias que representan. Para Informatica, el **dinero** y **smallmoney** tipos de datos tienen una precisión de una centésima de las unidades monetarias que representan.
  
Use un punto para separar las unidades parciales de moneda, como céntimos, de las unidades completas de moneda. Por ejemplo, 2.15 puede especificar 2 dólares y 15 centavos.
  
Estos tipos de datos pueden usar alguno de los siguientes símbolos de moneda.
  
![Tabla de símbolos de moneda, valores hexadecimales](../../t-sql/data-types/media/money01.gif "tabla de símbolos de moneda, valores hexadecimales")
  
No es necesario incluir los datos de moneda entre comillas simples ('). Es importante recordar que aunque es posible especificar valores monetarios precedidos de un símbolo de moneda, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no almacena ninguna información de moneda asociada con el símbolo, solo almacena el valor numérico.
  
## <a name="converting-money-data"></a>Convertir datos money
Cuando se convierte a **dinero** de tipos de datos enteros, se suponen unidades en unidades de moneda. Por ejemplo, el valor entero 4 se convierte en el **dinero** equivalente de 4 unidades monetarias.
  
El ejemplo siguiente se convierte **smallmoney** y **dinero** valores **varchar** y **decimal** tipos de datos, respectivamente.
  
```sql
DECLARE @mymoney_sm smallmoney = 3148.29,  
        @mymoney    money = 3148.29;  
SELECT  CAST(@mymoney_sm AS varchar) AS 'SM_MONEY varchar',  
        CAST(@mymoney AS decimal)    AS 'MONEY DECIMAL';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
SM_MONEY VARCHAR               MONEY DECIMAL  
------------------------------ ----------------------  
3148.29                        3148    
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) 
 [CAST y CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md) 
 [Crear una tabla &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md) 
 [Tipos de datos &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md) 
 [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
 [Establecer @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/set-local-variable-transact-sql.md) 
 [sys.types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

