---
title: Codificado de forma rígida las instrucciones SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], hard-coded
- hard-coded SQL statements [ODBC]
- SQL statements [ODBC], constructing
ms.assetid: e355f5f1-4f1a-4933-8c74-ee73e90d2d19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 383a81aea121882b334bbfdab806408ac0513893
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746243"
---
# <a name="hard-coded-sql-statements"></a>Instrucciones SQL codificadas de forma rígida
Las aplicaciones que realizan una tarea fija normalmente contienen las instrucciones SQL codificadas de forma rígida. Por ejemplo, un sistema de entrada de pedidos podría usar la siguiente llamada a pedidos de venta abiertos de lista:  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 Hay varias ventajas a las instrucciones SQL codificadas de forma rígida: puede probarse cuando se escribe la aplicación; son más fáciles de implementar que las instrucciones creadas en tiempo de ejecución; y simplifican la aplicación.  
  
 Usar parámetros de instrucciones y preparar las instrucciones proporcionan aún mejores formas de usar las instrucciones SQL codificadas de forma rígida. Por ejemplo, suponga que la tabla Parts contiene las columnas PartID, descripción y precio. Sería una manera de insertar una nueva fila en esta tabla crear y ejecutar un **insertar** instrucción:  
  
```  
#define DESC_LEN 51  
#define STATEMENT_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN], Statement[STATEMENT_LEN];  
SQLREAL       Price;  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Build INSERT statement.  
sprintf_s(Statement, 100, "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (%d, '%s', %f)", PartID, Desc, Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 Una manera todavía mejor es usar una instrucción con parámetros codificados de forma rígida. Esto tiene dos ventajas a través de una instrucción con valores de datos codificados de forma rígida. En primer lugar, es más fácil de construir una instrucción parametrizada porque los valores de datos pueden enviarse en sus tipos nativos, como enteros y números de punto flotante, en lugar de convertirlas en cadenas. En segundo lugar, dicha instrucción se puede usar más de una vez basta con cambiar los valores de parámetro y deteniéndose No hay ninguna necesidad de volver a generarlo.  
  
```  
#define DESC_LEN 51  
  
SQLCHAR * Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 Suponiendo que esta instrucción se ejecute más de una vez, puede estar preparado para una eficacia todavía mayor:  
  
```  
#define DESC_LEN 51  
  
SQLCHAR *Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Prepare the INSERT statement.  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecute(hstmt);  
```  
  
 Quizás la forma más eficaz utilizar la instrucción es construir un procedimiento que contiene la instrucción, como se muestra en el siguiente ejemplo de código. Dado que el procedimiento se construye en tiempo de desarrollo y se almacenan en el origen de datos, no es necesario estar preparado en tiempo de ejecución. Un inconveniente de este método es que la sintaxis para crear procedimientos es específico de DBMS y los procedimientos deben crearse por separado para cada DBMS en el que es ejecutar la aplicación.  
  
```  
#define DESC_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecDirect(hstmt, "{call InsertPart(?, ?, ?)}", SQL_NTS);  
```  
  
 Para obtener más información acerca de los parámetros, las instrucciones preparadas y procedimientos, consulte [ejecutar una instrucción](../../../odbc/reference/develop-app/executing-a-statement.md).
