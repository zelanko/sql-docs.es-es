---
title: Recuperación de parámetros de salida mediante SQLGetData ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c96a3f9fc81d081ce16fe8e75746aafe8962fd0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294595"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>Recuperar parámetros de salida mediante SQLGetData
Antes de ODBC 3.8, una aplicación solo podía recuperar los parámetros de salida de una consulta con un búfer de salida enlazado. Sin embargo, es difícil asignar un búfer muy grande cuando el tamaño del valor del parámetro es muy grande (por ejemplo, una imagen grande). ODBC 3.8 introduce una nueva forma de recuperar parámetros de salida en partes. Una aplicación ahora puede llamar a **SQLGetData** con un búfer pequeño varias veces para recuperar un valor de parámetro grande. Esto es similar a la recuperación de datos de columnas grandes.  
  
 Para enlazar un parámetro de salida o un parámetro de entrada/salida que se va a recuperar en partes, llame a **SQLBindParameter** con el *InputOutputType* argumento establecido en SQL_PARAM_OUTPUT_STREAM o SQL_PARAM_INPUT_OUTPUT_STREAM. Con SQL_PARAM_INPUT_OUTPUT_STREAM, una aplicación puede usar **SQLPutData** para introducir datos en el parámetro y, a continuación, usar **SQLGetData** para recuperar el parámetro de salida. Los datos de entrada deben estar en el formulario de datos en ejecución (DAE), mediante **SQLPutData** en lugar de enlazarlos a un búfer preasignado.  
  
 Esta característica se puede usar en aplicaciones ODBC 3.8 o aplicaciones ODBC 3.x y ODBC 2.x recompiladas, y estas aplicaciones deben tener un controlador ODBC 3.8 que admita la recuperación de parámetros de salida mediante **SQLGetData** y el Administrador de controladores ODBC 3.8. Para obtener información sobre cómo habilitar una aplicación anterior para usar nuevas características ODBC, vea Matriz de [compatibilidad](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
## <a name="usage-example"></a>Ejemplo de uso  
 Por ejemplo, considere la posibilidad de ejecutar un procedimiento almacenado, **"CALL sp_f(?,?)**, donde ambos parámetros están enlazados como SQL_PARAM_OUTPUT_STREAM y el procedimiento almacenado no devuelve ningún conjunto de resultados (más adelante en este tema encontrará un escenario más complejo):  
  
1.  Para cada parámetro, llame a **SQLBindParameter** con *InputOutputType* establecido en SQL_PARAM_OUTPUT_STREAM y *ParameterValuePtr* establecido en un token, como un número de parámetro, un puntero a datos o un puntero a una estructura que la aplicación utiliza para enlazar parámetros de entrada. En este ejemplo se usará el parámetro ordinal como token.  
  
2.  Ejecute la consulta con **SQLExecDirect** o **SQLExecute**. se devolverán SQL_PARAM_DATA_AVAILABLE, lo que indica que hay parámetros de salida transmitidos disponibles para la recuperación.  
  
3.  Llame a **SQLParamData** para obtener el parámetro que está disponible para la recuperación. **SQLParamData** devolverá SQL_PARAM_DATA_AVAILABLE con el token del primer parámetro disponible, que se establece en **SQLBindParameter** (paso 1). El token se devuelve en el búfer al que apunta *ValuePtrPtr.*  
  
4.  Llame a **SQLGetData** con\_el argumento *Col*_or*Param_Num* establece en el parámetro ordinal para recuperar los datos del primer parámetro disponible. Si **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLState 01004 (datos truncados) y el tipo es longitud variable en el cliente y el servidor, hay más datos para recuperar del primer parámetro disponible. Puede seguir llamando a **SQLGetData** hasta que devuelva SQL_SUCCESS o SQL_SUCCESS_WITH_INFO con un **SQLState**diferente.  
  
5.  Repita los pasos 3 y 4 para recuperar el parámetro actual.  
  
6.  Llame a **SQLParamData** de nuevo. Si devuelve algo excepto SQL_PARAM_DATA_AVAILABLE, no hay más datos de parámetro sortransmitidos para recuperar y el código de retorno será el código de retorno de la siguiente instrucción que se ejecuta.  
  
7.  Llame a **SQLMoreResults** para procesar el siguiente conjunto de parámetros hasta que devuelve SQL_NO_DATA. **SQLMoreResults** devolverá SQL_NO_DATA en este ejemplo si el atributo de instrucción SQL_ATTR_PARAMSET_SIZE se estableció en 1. De lo contrario, **SQLMoreResults** devolverá SQL_PARAM_DATA_AVAILABLE para indicar que hay parámetros de salida transmitidos disponibles para el siguiente conjunto de parámetros que se va a recuperar.  
  
 Similar a un parámetro de entrada DAE, el token utilizado en el argumento *ParameterValuePtr* en **SQLBindParameter** (paso 1) puede ser un puntero que apunta a una estructura de datos de aplicación, que contiene el ordinal del parámetro y más información específica de la aplicación, si es necesario.  
  
 El orden de la salida transmitida devuelta o los parámetros de entrada/salida es específico del controlador y puede que no siempre sea el mismo que el orden especificado en la consulta.  
  
 Si la aplicación no llama a **SQLGetData** en el paso 4, se descarta el valor del parámetro. De forma similar, si la aplicación llama a **SQLParamData** antes de que **SQLGetData**haya leído todo un valor de parámetro, se descarta el resto del valor y la aplicación puede procesar el siguiente parámetro.  
  
 Si la aplicación llama a **SQLMoreResults** antes de que se procesen todos los parámetros de salida transmitidos **(SQLParamData** sigue devolviendo SQL_PARAM_DATA_AVAILABLE), se descartan todos los parámetros restantes. De forma similar, si la aplicación llama a **SQLMoreResults** antes de que **SQLGetData**haya leído todo un valor de parámetro, se descartan el resto del valor y todos los parámetros restantes y la aplicación puede continuar procesando el siguiente conjunto de parámetros.  
  
 Tenga en cuenta que una aplicación puede especificar el tipo de datos C en **SQLBindParameter** y **SQLGetData**. El tipo de datos de C especificado con **SQLGetData** reemplaza el tipo de datos de C especificado en **SQLBindParameter**, a menos que el tipo de datos de C especificado en **SQLGetData** se SQL_APD_TYPE.  
  
 Aunque un parámetro de salida transmitido por secuencias es más útil cuando el tipo de datos del parámetro de salida es de tipo BLOB, esta funcionalidad también se puede usar con cualquier tipo de datos. Los tipos de datos admitidos por los parámetros de salida transmitidos se especifican en el controlador.  
  
 Si hay SQL_PARAM_INPUT_OUTPUT_STREAM parámetros que se van a procesar, **SQLExecute** o **SQLExecDirect** devolverá SQL_NEED_DATA primero. Una aplicación puede llamar a **SQLParamData** y **SQLPutData** para enviar datos de parámetros DAE. Cuando se procesan todos los parámetros de entrada DAE, **SQLParamData** devuelve SQL_PARAM_DATA_AVAILABLE para indicar que los parámetros de salida transmitidos están disponibles.  
  
 Cuando hay parámetros de salida transmitidos y parámetros de salida enlazados que se van a procesar, el controlador determina el orden para procesar los parámetros de salida. Por lo tanto, si un parámetro de salida está enlazado a un búfer (el parámetro **SQLBindParameter** *InputOutputType* se establece en SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT), es posible que el búfer no se rellene hasta que **SQLParamData** devuelva SQL_SUCCESS o SQL_SUCCESS_WITH_INFO. Una aplicación debe leer un búfer enlazado solo después de **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO que es después de que se procesan todos los parámetros de salida transmitidos.  
  
 El origen de datos puede devolver una advertencia y un conjunto de resultados, además del parámetro de salida transmitido. En general, las advertencias y los conjuntos de resultados se procesan por separado de un parámetro de salida transmitido llamando a **SQLMoreResults**. Procesar advertencias y el conjunto de resultados antes de procesar el parámetro de salida transmitido.  
  
 En la tabla siguiente se describen diferentes escenarios de un único comando enviado al servidor y cómo debe funcionar la aplicación.  
  
|Escenario|Valor devuelto de SQLExecute o SQLExecDirect|Pasos siguientes|  
|--------------|---------------------------------------------------|---------------------|  
|Los datos solo incluyen parámetros de salida transmitidos|SQL_PARAM_DATA_AVAILABLE|Use **SQLParamData** y **SQLGetData** para recuperar parámetros de salida transmitidos.|  
|Los datos incluyen un conjunto de resultados y parámetros de salida transmitidos|SQL_SUCCESS|Recupere el conjunto de resultados con **SQLBindCol** y **SQLGetData**.<br /><br /> Llame a **SQLMoreResults** para iniciar el procesamiento de parámetros de salida transmitidos. Debería devolver SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** y **SQLGetData** para recuperar parámetros de salida transmitidos.|  
|Los datos incluyen un mensaje de advertencia y parámetros de salida transmitidos|SQL_SUCCESS_WITH_INFO|Use **SQLGetDiagRec** y **SQLGetDiagField** para procesar mensajes de advertencia.<br /><br /> Llame a **SQLMoreResults** para iniciar el procesamiento de parámetros de salida transmitidos. Debería devolver SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** y **SQLGetData** para recuperar parámetros de salida transmitidos.|  
|Los datos incluyen un mensaje de advertencia, un conjunto de resultados y parámetros de salida transmitidos|SQL_SUCCESS_WITH_INFO|Use **SQLGetDiagRec** y **SQLGetDiagField** para procesar mensajes de advertencia. A continuación, llame a **SQLMoreResults** para empezar a procesar el conjunto de resultados.<br /><br /> Recuperar un conjunto de resultados con **SQLBindCol** y **SQLGetData**.<br /><br /> Llame a **SQLMoreResults** para iniciar el procesamiento de parámetros de salida transmitidos. **SQLMoreResults** debe devolver SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** y **SQLGetData** para recuperar parámetros de salida transmitidos.|  
|Consultar con parámetros de entrada DAE, por ejemplo, un parámetro de entrada/salida (DAE) transmitido|SQL NEED_DATA|Llame a **SQLParamData** y **SQLPutData** para enviar datos de parámetros de entrada DAE.<br /><br /> Después de procesar todos los parámetros de entrada de DAE, **SQLParamData** puede devolver cualquier código de retorno que **SQLExecute** y **SQLExecDirect** pueden devolver. A continuación, se pueden aplicar los casos de esta tabla.<br /><br /> Si el código de retorno es SQL_PARAM_DATA_AVAILABLE, los parámetros de salida transmitidos están disponibles. Una aplicación debe llamar a **SQLParamData** de nuevo para recuperar el token para el parámetro de salida transmitido, como se describe en la primera fila de esta tabla.<br /><br /> Si el código de retorno es SQL_SUCCESS, hay un conjunto de resultados para procesar o se completa el procesamiento.<br /><br /> Si el código de retorno es SQL_SUCCESS_WITH_INFO, hay mensajes de advertencia para procesar.|  
  
 Después de **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** devuelve SQL_PARAM_DATA_AVAILABLE, se producirá un error de secuencia de función si una aplicación llama a una función que no está en la lista siguiente:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagrec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (con identificador de instrucción)  
  
-   **SQLFreeStmt** (con Opción SQL_CLOSE, SQL_DROP o SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (con HandleType - SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 Las aplicaciones todavía pueden usar **SQLSetDescField** o **SQLSetDescRec** para establecer la información de enlace. La asignación de campos no se cambiará. Sin embargo, los campos dentro del descriptor pueden devolver nuevos valores. Por ejemplo, SQL_DESC_PARAMETER_TYPE podría devolver SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>Escenario de uso: recuperar una imagen en partes de un conjunto de resultados  
 **SQLGetData** se puede usar para obtener datos en partes cuando un procedimiento almacenado devuelve un conjunto de resultados que contiene una fila de metadatos sobre una imagen y la imagen se devuelve en un parámetro de salida grande.  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>Escenario de uso: Enviar y recibir un objeto grande como parámetro de entrada/salida transmitido  
 **SQLGetData** se puede usar para obtener y enviar datos en partes cuando un procedimiento almacenado pasa un objeto grande como un parámetro de entrada/salida, transmitiendo el valor hacia y desde la base de datos. No es necesario almacenar todos los datos en la memoria.  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md)
