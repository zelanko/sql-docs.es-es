---
title: Recuperación de parámetros de salida mediante SQLGetData | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eeb8fae9c563e675499dec47839acdd0a003765a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020510"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>Recuperar parámetros de salida mediante SQLGetData
Antes de ODBC 3,8, una aplicación solo podía recuperar los parámetros de salida de una consulta con un búfer de salida enlazado. Sin embargo, es difícil asignar un búfer muy grande cuando el tamaño del valor del parámetro es muy grande (por ejemplo, una imagen grande). ODBC 3,8 presenta una nueva manera de recuperar los parámetros de salida en partes. Una aplicación ahora puede llamar a **SQLGetData** con un búfer pequeño varias veces para recuperar un valor de parámetro grande. Esto es similar a la recuperación de datos de columnas grandes.  
  
 Para enlazar un parámetro de salida o parámetro de entrada y salida que se va a recuperar en partes, llame a **SQLBindParameter** con el argumento *InputOutputType* establecido en SQL_PARAM_OUTPUT_STREAM o SQL_PARAM_INPUT_OUTPUT_STREAM. Con SQL_PARAM_INPUT_OUTPUT_STREAM, una aplicación puede utilizar **SQLPutData** para introducir datos en el parámetro y, a continuación, usar **SQLGetData** para recuperar el parámetro de salida. Los datos de entrada deben estar en el formato de datos en ejecución (DAE) mediante **SQLPutData** en lugar de enlazarlos a un búfer preasignado.  
  
 Esta característica se puede usar en aplicaciones ODBC 3,8 o en aplicaciones ODBC 3. x y ODBC 2. x compiladas, y estas aplicaciones deben tener un controlador ODBC 3,8 que admita la recuperación de parámetros de salida mediante el administrador de controladores de **SQLGetData** y ODBC 3,8. Para obtener información sobre cómo habilitar una aplicación anterior para que use las nuevas características ODBC, vea [matriz de compatibilidad](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
## <a name="usage-example"></a>Ejemplo de uso  
 Por ejemplo, considere la posibilidad de ejecutar un procedimiento almacenado, **{CALL sp_f (?,?)}**, donde ambos parámetros se enlazan como SQL_PARAM_OUTPUT_STREAM y el procedimiento almacenado no devuelve ningún conjunto de resultados (más adelante en este tema encontrará un escenario más complejo):  
  
1.  Para cada parámetro, llame a **SQLBindParameter** con *InputOutputType* establecido en SQL_PARAM_OUTPUT_STREAM y *ParameterValuePtr* establecido en un token, como un número de parámetro, un puntero a datos o un puntero a una estructura que la aplicación usa para enlazar parámetros de entrada. En este ejemplo se usará el parámetro ordinal como el token.  
  
2.  Ejecute la consulta con **SQLExecDirect** o **SQLExecute**. Se devolverá SQL_PARAM_DATA_AVAILABLE, lo que indica que hay parámetros de salida transmitidos disponibles para la recuperación.  
  
3.  Llame a **SQLParamData** para obtener el parámetro que está disponible para la recuperación. **SQLParamData** devolverá SQL_PARAM_DATA_AVAILABLE con el token del primer parámetro disponible, que se establece en **SQLBindParameter** (paso 1). El token se devuelve en el búfer al que apunta *ValuePtrPtr* .  
  
4.  Llame a **SQLGetData** con el argumento *col*_or\_*Param_Num* establecido en el ordinal del parámetro para recuperar los datos del primer parámetro disponible. Si **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos truncados) y el tipo es de longitud variable tanto en el cliente como en el servidor, hay más datos que recuperar del primer parámetro disponible. Puede seguir llamando a **SQLGetData** hasta que devuelva SQL_SUCCESS o SQL_SUCCESS_WITH_INFO con un **SQLSTATE**diferente.  
  
5.  Repita los pasos 3 y 4 para recuperar el parámetro actual.  
  
6.  Vuelva a llamar a **SQLParamData** . Si devuelve algo excepto SQL_PARAM_DATA_AVAILABLE, no hay más datos de parámetros transmitidos para recuperar y el código de retorno será el código de retorno de la siguiente instrucción que se ejecuta.  
  
7.  Llame a **SQLMoreResults** para procesar el siguiente conjunto de parámetros hasta que devuelva SQL_NO_DATA. **SQLMoreResults** devolverá SQL_NO_DATA en este ejemplo si el atributo Statement SQL_ATTR_PARAMSET_SIZE se estableció en 1. De lo contrario, **SQLMoreResults** devolverá SQL_PARAM_DATA_AVAILABLE para indicar que hay parámetros de salida transmitidos disponibles para el siguiente conjunto de parámetros que se van a recuperar.  
  
 Similar a un parámetro de entrada de DAE, el token usado en el argumento *ParameterValuePtr* de **SQLBindParameter** (paso 1) puede ser un puntero que apunta a una estructura de datos de aplicación, que contiene el ordinal del parámetro y más información específica de la aplicación, si es necesario.  
  
 El orden de los parámetros de entrada y salida transmitidos es específico del controlador y es posible que no siempre coincida con el orden especificado en la consulta.  
  
 Si la aplicación no llama a **SQLGetData** en el paso 4, se descarta el valor del parámetro. Del mismo modo, si la aplicación llama a **SQLParamData** antes de que **SQLGetData**haya leído todos los valores de parámetro, se descarta el resto del valor y la aplicación puede procesar el parámetro siguiente.  
  
 Si la aplicación llama a **SQLMoreResults** antes de que se procesen todos los parámetros de salida transmitidos (**SQLParamData** sigue devolviendo SQL_PARAM_DATA_AVAILABLE), se descartan todos los parámetros restantes. Del mismo modo, si la aplicación llama a **SQLMoreResults** antes de que **SQLGetData**haya leído todos los valores de parámetro, el resto del valor y todos los parámetros restantes se descartan y la aplicación puede continuar procesando el siguiente conjunto de parámetros.  
  
 Tenga en cuenta que una aplicación puede especificar el tipo de datos C en **SQLBindParameter** y **SQLGetData**. El tipo de datos C especificado con **SQLGetData** invalida el tipo de datos c especificado en **SQLBindParameter**, a menos que se SQL_APD_TYPE el tipo de datos c especificado en **SQLGetData** .  
  
 Aunque un parámetro de salida transmitido es más útil cuando el tipo de datos del parámetro de salida es de tipo BLOB, esta funcionalidad también se puede usar con cualquier tipo de datos. Los tipos de datos admitidos por los parámetros de salida transmitidos se especifican en el controlador.  
  
 Si hay SQL_PARAM_INPUT_OUTPUT_STREAM parámetros que se van a procesar, **SQLExecute** o **SQLExecDirect** devolverán SQL_NEED_DATA primero. Una aplicación puede llamar a **SQLParamData** y **SQLPutData** para enviar datos de parámetros de DAE. Cuando se procesan todos los parámetros de entrada de DAE, **SQLParamData** devuelve SQL_PARAM_DATA_AVAILABLE para indicar que los parámetros de salida transmitidos están disponibles.  
  
 Cuando hay parámetros de salida transmitidos por secuencias y parámetros de salida enlazados que se van a procesar, el controlador determina el orden de procesamiento de los parámetros de salida. Por lo tanto, si un parámetro de salida se enlaza a un búfer (el parámetro **SQLBindParameter** *InputOutputType* se establece en SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT), el búfer no se puede rellenar hasta que **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO. Una aplicación debe leer un búfer enlazado solo después de que **SQLParamData** devuelva SQL_SUCCESS o SQL_SUCCESS_WITH_INFO que sea después de que se procesen todos los parámetros de salida transmitidos.  
  
 El origen de datos puede devolver una advertencia y un conjunto de resultados, además del parámetro de salida transmitido. En general, las advertencias y los conjuntos de resultados se procesan de forma independiente de un parámetro de salida transmitido mediante una llamada a **SQLMoreResults**. Procese las advertencias y el conjunto de resultados antes de procesar el parámetro de salida transmitido.  
  
 En la tabla siguiente se describen los distintos escenarios de un solo comando que se envía al servidor y cómo debe funcionar la aplicación.  
  
|Escenario|Valor devuelto de SQLExecute o SQLExecDirect|Qué hacer después|  
|--------------|---------------------------------------------------|---------------------|  
|Los datos solo incluyen parámetros de salida transmitidos|SQL_PARAM_DATA_AVAILABLE|Use **SQLParamData** y **SQLGetData** para recuperar los parámetros de salida transmitidos por secuencias.|  
|Los datos incluyen un conjunto de resultados y parámetros de salida transmitidos|SQL_SUCCESS|Recupere el conjunto de resultados con **SQLBindCol** y **SQLGetData**.<br /><br /> Llame a **SQLMoreResults** para iniciar el procesamiento de los parámetros de salida transmitidos. Debe devolver SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** y **SQLGetData** para recuperar los parámetros de salida transmitidos por secuencias.|  
|Los datos incluyen un mensaje de advertencia y parámetros de salida transmitidos|SQL_SUCCESS_WITH_INFO|Use **SQLGetDiagRec** y **SQLGetDiagField** para procesar los mensajes de advertencia.<br /><br /> Llame a **SQLMoreResults** para iniciar el procesamiento de los parámetros de salida transmitidos. Debe devolver SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** y **SQLGetData** para recuperar los parámetros de salida transmitidos por secuencias.|  
|Los datos incluyen un mensaje de advertencia, un conjunto de resultados y parámetros de salida transmitidos|SQL_SUCCESS_WITH_INFO|Use **SQLGetDiagRec** y **SQLGetDiagField** para procesar los mensajes de advertencia. A continuación, llame a **SQLMoreResults** para iniciar el procesamiento del conjunto de resultados.<br /><br /> Recupere un conjunto de resultados con **SQLBindCol** y **SQLGetData**.<br /><br /> Llame a **SQLMoreResults** para iniciar el procesamiento de los parámetros de salida transmitidos. **SQLMoreResults** debe devolver SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** y **SQLGetData** para recuperar los parámetros de salida transmitidos por secuencias.|  
|Consulta con parámetros de entrada de DAE, por ejemplo, un parámetro de entrada/salida (DAE) transmitido|NEED_DATA SQL|Llame a **SQLParamData** y **SQLPutData** para enviar los datos del parámetro de entrada del DAE.<br /><br /> Una vez procesados todos los parámetros de entrada del DAE, **SQLParamData** puede devolver cualquier código de retorno que devuelva **SQLExecute** y **SQLExecDirect** . A continuación, se pueden aplicar los casos de esta tabla.<br /><br /> Si el código de retorno es SQL_PARAM_DATA_AVAILABLE, los parámetros de salida transmitidos están disponibles. Una aplicación debe volver a llamar a **SQLParamData** para recuperar el token para el parámetro de salida transmitido, tal y como se describe en la primera fila de esta tabla.<br /><br /> Si el código de retorno es SQL_SUCCESS, significa que hay un conjunto de resultados que se va a procesar o que se ha completado el procesamiento.<br /><br /> Si el código de retorno es SQL_SUCCESS_WITH_INFO, hay mensajes de advertencia que se van a procesar.|  
  
 Después de que **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** devuelvan SQL_PARAM_DATA_AVAILABLE, se producirá un error de secuencia de función si una aplicación llama a una función que no está en la lista siguiente:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **** SQLGetEnvAttr / **** SQLGetDescField / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (con identificador de instrucción)  
  
-   **SQLFreeStmt** (con Option = SQL_CLOSE, SQL_DROP o SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (con HandleType = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 Las aplicaciones pueden seguir usando **SQLSetDescField** o **SQLSetDescRec** para establecer la información de enlace. No se cambiará la asignación de campos. Sin embargo, los campos incluidos en el descriptor podrían devolver nuevos valores. Por ejemplo, SQL_DESC_PARAMETER_TYPE podría devolver SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>Escenario de uso: recuperación de una imagen de elementos de un conjunto de resultados  
 **SQLGetData** se puede utilizar para obtener datos en elementos cuando un procedimiento almacenado devuelve un conjunto de resultados que contiene una fila de metadatos sobre una imagen y la imagen se devuelve en un parámetro de salida grande.  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>Escenario de uso: enviar y recibir un objeto grande como un parámetro de entrada/salida transmitido  
 **SQLGetData** se puede utilizar para obtener y enviar datos en elementos cuando un procedimiento almacenado pasa un objeto grande como un parámetro de entrada/salida, que transmite el valor a y desde la base de datos. No es necesario almacenar todos los datos en la memoria.  
  
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
