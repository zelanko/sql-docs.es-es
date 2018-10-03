---
title: Uso de longitud y valores de indicador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 442d0865ede4819ea3413d662411295daa5b48bd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646023"
---
# <a name="using-length-and-indicator-values"></a>Uso de longitud y valores de indicador
El búfer de longitud/indicador se usa para pasar la longitud de bytes de los datos en el búfer de datos o un indicador especial como SQL_NULL_DATA, lo que indica que los datos son NULL. Dependiendo de la función en el que se utiliza, un búfer de longitud/indicador se define como un SQLINTEGER o un SQLSMALLINT. Por lo tanto, se necesita un único argumento para describirlo. Si el búfer de datos es un búfer de entrada nondeferred, este argumento contiene la longitud de bytes de los propios datos o un valor de indicador. A menudo se denomina *StrLen_or_Ind* o un nombre similar. Por ejemplo, el siguiente código llama a **SQLPutData** para pasar un búfer lleno de datos; la longitud de bytes (*ValueLen*) se pasa directamente porque el búfer de datos (*ValuePtr*) es un búfer de entrada.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 Si el búfer de datos es un búfer de entrada aplazado, un búfer de salida nondeferred o un búfer de salida, el argumento contiene la dirección del búfer de longitud/indicador. A menudo se denomina *StrLen_or_IndPtr* o un nombre similar. Por ejemplo, el siguiente código llama a **SQLGetData** para recuperar un búfer lleno de datos; la longitud de bytes que se devuelve a la aplicación en el búfer de longitud/indicador (*ValueLenOrInd*), cuya dirección es pasa a **SQLGetData** porque el búfer de datos correspondiente (*ValuePtr*) es un búfer de salida nondeferred.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A menos que se prohíbe en concreto, un argumento de búfer de longitud/indicador puede ser 0 (si entrada nondeferred) o un puntero nulo (si salida o entrada diferida). Para los búferes de entrada, esto hace que el controlador pasar por alto la longitud de bytes de los datos. Esto devuelve un error al pasar los datos de longitud variable, pero es habitual cuando se pasan datos distintos de null, de longitud fija, ya que se necesita una longitud ni un valor de indicador. Para los búferes de salida, esto hace que el controlador no devuelve la longitud de bytes de los datos o un valor de indicador. Se trata de un error si los datos devueltos por el controlador es NULL, pero es habituales cuando se recuperan datos de longitud fija, que no acepta valores NULL, ya que se necesita una longitud ni un valor de indicador.  
  
 Como cuando la dirección de un búfer de datos aplazado se pasa al controlador, la dirección de un búfer de longitud/indicador aplazada debe seguir siendo válida hasta que el búfer es independiente.  
  
 Las longitudes de los siguientes son válidas como valores de longitud/indicador:  
  
-   *n*, donde *n* > 0.  
  
-   0.  
  
-   SQL_NTS. Una cadena que se envían al controlador en el búfer de datos correspondiente está terminada en null; se trata de una manera conveniente para los programadores de C pasar cadenas sin tener que calcular su longitud en bytes. Este valor es válido únicamente cuando la aplicación envía datos al controlador. Cuando el controlador devuelve datos a la aplicación, siempre devuelve la longitud real de bytes de los datos.  
  
 Los valores siguientes son válidos como valores de indicador de longitud. SQL_NULL_DATA se almacena en el campo de descriptor SQL_DESC_INDICATOR_PTR; todos los demás valores se almacenan en el campo de descriptor SQL_DESC_OCTET_LENGTH_PTR.  
  
-   SQL_NULL_DATA. Los datos están un valor de datos es NULL, y se omite el valor en el búfer de datos correspondiente. Este valor es válido únicamente para datos de SQL enviados a o se recupera desde el controlador.  
  
-   SQL_DATA_AT_EXEC. El búfer de datos no contiene ningún dato. En su lugar, los datos se enviarán con **SQLPutData** cuando se ejecuta la instrucción o cuando **SQLBulkOperations** o **SQLSetPos** se llama. Este valor es válido sólo para los datos SQL enviados al controlador. Para obtener más información, consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), y [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro. Este valor es similar a SQL_DATA_AT_EXEC. Para obtener más información, consulte [enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. El controlador no puede determinar el número de bytes de datos long siguen disponibles para devolver en un búfer de salida. Este valor es válido sólo para recuperar desde el controlador de datos de SQL.  
  
-   SQL_DEFAULT_PARAM. Un procedimiento consiste en utilizar el valor predeterminado de un parámetro de entrada en un procedimiento en lugar del valor en el búfer de datos correspondiente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** o **SQLSetPos** va a omitir el valor en el búfer de datos. Al actualizar una fila de datos mediante una llamada a **SQLBulkOperations** o **SQLSetPos,** no se cambia el valor de columna. Cuando se inserta una nueva fila de datos mediante una llamada a **SQLBulkOperations**, el valor de columna se establece en su valor predeterminado o, si la columna no tiene valor predeterminado, null.
