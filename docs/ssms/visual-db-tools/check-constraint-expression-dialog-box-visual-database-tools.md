---
title: "Cuadro de diálogo de la expresión de restricción CHECK (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vdt.dlgbox.checkconstraintexpression
ms.assetid: beb6ce43-3913-4d66-8826-8e885335b790
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7cf57c1f37b4a18cb43935e1f2108933a861233
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="check-constraint-expression-dialog-box-visual-database-tools"></a>Expresión de restricción CHECK (cuadro de diálogo, Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Cuando adjunte una restricción CHECK a una tabla o columna, debe incluir una expresión SQL. Escriba la expresión de restricción CHECK en el cuadro correspondiente.  
  
## <a name="uielement-list"></a>Lista de UIElement  
Expresión  
Escriba la expresión.  
  
Puede crear una expresión de restricción sencilla para comprobar una condición sencilla en los datos o puede crear una expresión compleja mediante operadores booleanos para comprobar varias condiciones en los datos. Por ejemplo, supongamos que la tabla authors tiene una columna zip que requiere una cadena de caracteres de 5 dígitos. Esta expresión de restricción de ejemplo garantiza que solo se permitan números de 5 dígitos:  
  
```  
zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
```  
  
O bien, supongamos que la tabla sales tiene una columna llamada qty que requiere un valor mayor que 0. Esta restricción de muestra garantiza que solo se permitan los valores positivos:  
  
```  
qty > 0  
```  
  
Supongamos también que la tabla orders limita el tipo de tarjetas de crédito admitidas para todos los pedidos de tarjeta de crédito. Esta restricción de ejemplo garantiza que si el pedido se realiza con una tarjeta de crédito, solo se aceptará Visa, MasterCard o American Express:  
  
```  
NOT (payment_method = 'credit card') OR  
   (card_type IN ('VISA', 'MASTERCARD', 'AMERICAN EXPRESS'))  
```  
  
## <a name="to-define-a-constraint-expression"></a>Para definir una expresión de restricción  
En la pestaña Restricciones CHECK de las páginas de propiedades, escriba una expresión en el cuadro de diálogo Expresión de restricción CHECK utilizando la sintaxis siguiente:  
  
<pre>{constant | column_name | function | (subquery)}  
[{operator | AND | OR | NOT}  
{constant | column_name | function | (subquery)}...]</pre>  
  
La sintaxis de SQL está formada por los siguientes parámetros:  
  
|Parámetro|Description|  
|-------------|---------------|  
|constant|Valor literal, como un valor numérico o una cadena de caracteres. Los datos de caracteres deben escribirse entre comillas sencillas (').|  
|column_name|Especifica una columna.|  
|function|Función integrada.|  
|operador|Operadores aritméticos, bit a bit, de comparación o de cadena.|  
|y|Se utiliza en expresiones booleanas para conectar dos expresiones. Se devuelven resultados cuando las dos expresiones son verdaderas.<br /><br />Cuando se utilizan los operadores AND y OR en una instrucción, se procesará primero el operador AND. Puede cambiar el orden de ejecución utilizando paréntesis.|  
|O BIEN|Se utiliza en expresiones booleanas para conectar dos o más condiciones. Se devuelven resultados cuando al menos una de las condiciones sea verdadera.<br /><br />Cuando se utilizan los operadores AND y OR en una instrucción, OR se evaluará después de AND. Puede cambiar el orden de ejecución utilizando paréntesis.|  
|NOT|Niega cualquier expresión booleana (que puede incluir palabras clave como LIKE, NULL, BETWEEN, IN y EXISTS).<br /><br />Cuando se utiliza más de un operador lógico en una instrucción, se procesará primero el operador NOT. Puede cambiar el orden de ejecución utilizando paréntesis.|  
  
## <a name="see-also"></a>Ver también  
[Restricciones UNIQUE y restricciones CHECK](http://msdn.microsoft.com/en-us/637098af-2567-48f8-90f4-b41df059833e)  
[Crear restricciones UNIQUE](http://msdn.microsoft.com/en-us/a86f9d6f-f242-43be-b65d-b3435b71b62a)  
  
