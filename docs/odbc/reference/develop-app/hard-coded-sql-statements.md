---
title: Codificado de forma rígida instrucciones SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], hard-coded
- hard-coded SQL statements [ODBC]
- SQL statements [ODBC], constructing
ms.assetid: e355f5f1-4f1a-4933-8c74-ee73e90d2d19
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab17362cdece97582e26e6bc99ed38e678db6a4c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="hard-coded-sql-statements"></a>Instrucciones SQL codificadas de forma rígida
Las aplicaciones que realizan una tarea fija normalmente contienen instrucciones de SQL codificadas de forma rígida. Por ejemplo, un sistema de entrada de pedidos puede usar la siguiente llamada a pedidos de ventas abiertos de lista:  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 Hay varias ventajas con respecto a las instrucciones de SQL codificadas de forma rígida: puede probarse cuando se escribe la aplicación; son más fáciles de implementar que las instrucciones creadas en tiempo de ejecución; y simplifican la aplicación.  
  
 Usar parámetros de instrucciones y preparación de instrucciones proporcionan formas aún mejor usar instrucciones de SQL codificadas de forma rígida. Por ejemplo, suponga que la tabla Parts contiene las columnas PartID, descripción y el precio. Una forma para insertar una nueva fila en esta tabla sería generar y ejecutar un **insertar** instrucción:  
  
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
  
 Una manera incluso más recomendable hacerlo es usar una instrucción con parámetros codificados de forma rígida. Esto tiene dos ventajas con respecto a una instrucción con valores de datos codificados de forma rígida. En primer lugar, es más fácil construir una instrucción con parámetros porque los valores de datos se pueden enviar en sus tipos nativos, como enteros y números de punto flotante, en lugar de convertirlos en cadenas. En segundo lugar, una instrucción de este tipo se puede utilizar más de una vez basta con cambiar los valores de parámetro y volver a ejecutar no es necesario volver a crearla.  
  
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
  
 Suponiendo que esta instrucción que se ejecute más de una vez, se pueden preparar para mayor eficacia:  
  
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
  
 Quizás la forma más eficaz utilizar la instrucción es crear un procedimiento que contiene la instrucción, como se indica en el siguiente ejemplo de código. Dado que el procedimiento se crea en tiempo de desarrollo y almacenado en el origen de datos, no es necesario estar preparado en tiempo de ejecución. El inconveniente de este método es que la sintaxis para crear procedimientos específicos de DBMS y procedimientos deben crearse por separado para cada DBMS en el que es ejecutar la aplicación.  
  
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
  
 Para obtener más información sobre los parámetros, instrucciones preparadas y procedimientos, consulte [ejecutar una instrucción](../../../odbc/reference/develop-app/executing-a-statement.md).
