---
title: Usar valores de longitud y indicador | Microsoft Docs
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
ms.openlocfilehash: b3a0b54617d55033addabc729adbd078680022fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67902470"
---
# <a name="using-length-and-indicator-values"></a>Uso de longitud y valores de indicador
El búfer de longitud/indicador se usa para pasar la longitud de bytes de los datos en el búfer de datos o un indicador especial como SQL_NULL_DATA, que indica que los datos son NULL. Dependiendo de la función en la que se usa, se define un búfer de longitud/indicador como SQLINTEGER donde o SQLSMALLINT. Por lo tanto, se necesita un único argumento para describirlo. Si el búfer de datos es un búfer de entrada nondeferred, este argumento contiene la longitud de bytes de los datos en sí o un valor de indicador. A menudo se denomina *StrLen_or_Ind* o un nombre similar. Por ejemplo, el siguiente código llama a **SQLPutData** para pasar un búfer lleno de datos; la longitud de bytes (*ValueLen*) se pasa directamente porque el búfer de datos (*ValuePtr*) es un búfer de entrada.  
  
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
  
 Si el búfer de datos es un búfer de entrada aplazado, un búfer de salida de nondeferred o un búfer de salida, el argumento contiene la dirección del búfer de longitud/indicador. A menudo se denomina *StrLen_or_IndPtr* o un nombre similar. Por ejemplo, el código siguiente llama a **SQLGetData** para recuperar un búfer lleno de datos; la longitud de bytes se devuelve a la aplicación en el búfer de longitud/indicador (*ValueLenOrInd*), cuya dirección se pasa a **SQLGetData** porque el búfer de datos correspondiente (*ValuePtr*) es un búfer de salida de nondeferred.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A menos que esté prohibida específicamente, un argumento de búfer de longitud/indicador puede ser 0 (si la entrada nondeferred) o un puntero NULL (si se trata de una entrada de salida o diferida). En el caso de los búferes de entrada, esto hace que el controlador omita la longitud de bytes de los datos. Esto devuelve un error al pasar datos de longitud variable, pero es común cuando se pasan datos de longitud fija no NULL, ya que no se necesita ni un valor de longitud ni un indicador. En el caso de los búferes de salida, esto hace que el controlador no devuelva la longitud de bytes de los datos o un valor de indicador. Se trata de un error si los datos devueltos por el controlador son NULL pero es común al recuperar datos de longitud fija, que no aceptan valores NULL, ya que no se necesita ni un valor de longitud ni un indicador.  
  
 Al igual que cuando se pasa la dirección de un búfer de datos diferido al controlador, la dirección de un búfer de indicador/longitud diferida debe ser válida hasta que se desenlace el búfer.  
  
 Las longitudes siguientes son válidas como valores de longitud/indicador:  
  
-   *n*, donde *n* > 0.  
  
-   0.  
  
-   SQL_NTS. Una cadena enviada al controlador en el búfer de datos correspondiente está terminada en null; Esta es una forma cómoda para que los programadores de C pasen cadenas sin tener que calcular su longitud de bytes. Este valor solo es válido cuando la aplicación envía datos al controlador. Cuando el controlador devuelve datos a la aplicación, siempre devuelve la longitud de bytes real de los datos.  
  
 Los valores siguientes son válidos como valores de longitud/indicador. SQL_NULL_DATA se almacena en el campo descriptor de SQL_DESC_INDICATOR_PTR; el resto de los valores se almacenan en el campo descriptor de SQL_DESC_OCTET_LENGTH_PTR.  
  
-   SQL_NULL_DATA. Los datos son un valor de datos NULL y se omite el valor del búfer de datos correspondiente. Este valor solo es válido para los datos SQL que se envían o se recuperan del controlador.  
  
-   SQL_DATA_AT_EXEC. El búfer de datos no contiene ningún dato. En su lugar, los datos se enviarán con **SQLPutData** cuando se ejecute la instrucción o cuando se llame a **SQLBulkOperations** o **SQLSetPos** . Este valor solo es válido para los datos SQL enviados al controlador. Para obtener más información, vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)y [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Resultado de la macro de SQL_LEN_DATA_AT_EXEC (*longitud*). Este valor es similar a SQL_DATA_AT_EXEC. Para obtener más información, consulte [envío de datos de tipo Long](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. El controlador no puede determinar el número de bytes de datos Long que siguen estando disponibles para su devolución en un búfer de salida. Este valor solo es válido para los datos SQL recuperados del controlador.  
  
-   SQL_DEFAULT_PARAM. Un procedimiento es usar el valor predeterminado de un parámetro de entrada en un procedimiento en lugar del valor del búfer de datos correspondiente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** o **SQLSetPos** es para omitir el valor en el búfer de datos. Al actualizar una fila de datos mediante una llamada a **SQLBulkOperations** o **SQLSetPos,** no se cambia el valor de la columna. Al insertar una nueva fila de datos mediante una llamada a **SQLBulkOperations**, el valor de la columna se establece en su valor predeterminado o, si la columna no tiene un valor predeterminado, en NULL.
