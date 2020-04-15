---
title: Uso de la longitud y los valores del indicador ( Length and Indicator Values) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0c878c9038b26aa996ed206c6b8adfe8d6c21e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306766"
---
# <a name="using-length-and-indicator-values"></a>Uso de longitud y valores de indicador
El búfer de longitud/indicador se utiliza para pasar la longitud de bytes de los datos en el búfer de datos o un indicador especial como SQL_NULL_DATA, que indica que los datos son NULL. Dependiendo de la función en la que se utilice, se define un búfer de longitud/indicador como SQLINTEGER o SQLSMALLINT. Por lo tanto, se necesita un único argumento para describirlo. Si el búfer de datos es un búfer de entrada no diferido, este argumento contiene la longitud de bytes de los datos en sí o un valor de indicador. A menudo se denomina *StrLen_or_Ind* o un nombre similar. Por ejemplo, el código siguiente llama a **SQLPutData** para pasar un búfer lleno de datos; la longitud de byte (*ValueLen*) se pasa directamente porque el búfer de datos (*ValuePtr*) es un búfer de entrada.  
  
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
  
 Si el búfer de datos es un búfer de entrada diferido, un búfer de salida no diferido o un búfer de salida, el argumento contiene la dirección del búfer de longitud/indicador. A menudo se denomina *StrLen_or_IndPtr* o un nombre similar. Por ejemplo, el código siguiente llama a **SQLGetData** para recuperar un búfer lleno de datos; la longitud de byte se devuelve a la aplicación en el búfer de longitud/indicador (*ValueLenOrInd*), cuya dirección se pasa a **SQLGetData** porque el búfer de datos correspondiente (*ValuePtr*) es un búfer de salida no diferido.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A menos que esté específicamente prohibido, un argumento de búfer de longitud/indicador puede ser 0 (si la entrada no diferida) o un puntero nulo (si la salida o la entrada diferida). Para los búferes de entrada, esto hace que el controlador ignore la longitud de bytes de los datos. Esto devuelve un error al pasar datos de longitud variable, pero es común cuando se pasan datos que no son nulos y de longitud fija, porque no se necesita ni una longitud ni un valor de indicador. Para los búferes de salida, esto hace que el controlador no devuelva la longitud de bytes de los datos o un valor de indicador. Se trata de un error si los datos devueltos por el controlador son NULL, pero es común al recuperar datos de longitud fija que no aceptan valores NULL, porque no se necesita ni una longitud ni un valor de indicador.  
  
 Al igual que cuando la dirección de un búfer de datos diferido se pasa al controlador, la dirección de un búfer de longitud/indicador diferido debe seguir siendo válida hasta que el búfer esté sin enlazar.  
  
 Las siguientes longitudes son válidas como valores de longitud/indicador:  
  
-   *n*, donde *n* > 0.  
  
-   0.  
  
-   SQL_NTS. Una cadena enviada al controlador en el búfer de datos correspondiente es terminada en null; esta es una manera conveniente para que los programadores de C pasen cadenas sin tener que calcular su longitud de bytes. Este valor es legal solo cuando la aplicación envía datos al controlador. Cuando el controlador devuelve datos a la aplicación, siempre devuelve la longitud de bytes real de los datos.  
  
 Los siguientes valores son válidos como valores de longitud/indicador. SQL_NULL_DATA se almacena en el campo descriptor de SQL_DESC_INDICATOR_PTR; todos los demás valores se almacenan en el campo descriptor de SQL_DESC_OCTET_LENGTH_PTR.  
  
-   SQL_NULL_DATA. Los datos son un valor de datos NULL y se omite el valor del búfer de datos correspondiente. Este valor solo es legal para los datos SQL enviados o recuperados desde el controlador.  
  
-   SQL_DATA_AT_EXEC. El búfer de datos no contiene ningún dato. En su lugar, los datos se enviarán con **SQLPutData** cuando se ejecuta la instrucción o cuando se llama a **SQLBulkOperations** o **SQLSetPos.** Este valor solo es legal para los datos SQL enviados al controlador. Para obtener más información, vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)y [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*). Este valor es similar a SQL_DATA_AT_EXEC. Para obtener más información, consulte [Envío de datos largos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. El controlador no puede determinar el número de bytes de datos largos todavía disponibles para devolver en un búfer de salida. Este valor solo es legal para los datos SQL recuperados del controlador.  
  
-   SQL_DEFAULT_PARAM. Un procedimiento consiste en utilizar el valor predeterminado de un parámetro de entrada en un procedimiento en lugar del valor del búfer de datos correspondiente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** o **SQLSetPos** debe omitir el valor en el búfer de datos. Al actualizar una fila de datos mediante una llamada a **SQLBulkOperations** o **SQLSetPos,** el valor de columna no se cambia. Al insertar una nueva fila de datos mediante una llamada a **SQLBulkOperations**, el valor de columna se establece en su valor predeterminado o, si la columna no tiene un valor predeterminado, en NULL.
