---
title: Matrices de parámetros de enlace | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597142d41ed8d3cff26891dfdcc89398543dab43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103823"
---
# <a name="binding-arrays-of-parameters"></a>Las matrices de parámetros de enlace
Las aplicaciones que utilizan las matrices de parámetros de enlazar las matrices a los parámetros en la instrucción SQL. Hay dos estilos de enlace:  
  
-   Enlazar una matriz para cada parámetro. Cada estructura de datos (matriz) contiene todos los datos de un solo parámetro. Esto se denomina *el enlace* porque se enlaza una columna de valores para un único parámetro.  
  
-   Definir una estructura que contenga los datos del parámetro para un conjunto completo de parámetros y enlazar una matriz de estas estructuras. Cada estructura de datos contiene los datos para una única instrucción SQL. Esto se denomina *el enlace* porque se enlaza a una fila de parámetros.  
  
 Cuando cuando la aplicación enlaza solo variables a parámetros, se llama a **SQLBindParameter** para enlazar las matrices de parámetros. La única diferencia es que las direcciones pasadas son direcciones de matriz, no solo-variable. La aplicación establece el atributo de instrucción SQL_ATTR_PARAM_BIND_TYPE para especificar si se trata de usar modo de columna (el valor predeterminado) o el enlace. Si se debe utilizar el enlace de columna o de modo de fila es principalmente una cuestión de preferencia de la aplicación. Dependiendo de cómo el procesador tiene acceso a la memoria, el enlace puede ser más rápido. Sin embargo, la diferencia es probable que sea insignificante, excepto un gran número de filas de parámetros.  
  
## <a name="column-wise-binding"></a>El enlace  
 Cuando se usa el enlace, una aplicación enlaza una o dos matrices para cada parámetro para el que son proporcionar datos. La primera matriz contiene los valores de datos, y la segunda matriz contiene los búferes de longitud/indicador. Cada matriz contiene tantos elementos como valores para el parámetro.  
  
 El enlace es el valor predeterminado. La aplicación también puede cambiar desde el enlace para el enlace estableciendo el atributo de instrucción SQL_ATTR_PARAM_BIND_TYPE. La siguiente ilustración muestra cómo el enlace funciona.  
  
 ![Muestra cómo columna&#45;inteligente enlace funciona](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 Por ejemplo, el código siguiente enlaza matrices de 10 elementos para los parámetros para las columnas PartID, descripción y precio y ejecuta una instrucción para insertar 10 filas. Usa el enlace.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
                                                "VALUES (?, ?, ?)";  
SQLUINTEGER    PartIDArray[ARRAY_SIZE];  
SQLCHAR        DescArray[ARRAY_SIZE][DESC_LEN];  
SQLREAL        PriceArray[ARRAY_SIZE];  
SQLINTEGER     PartIDIndArray[ARRAY_SIZE], DescLenOrIndArray[ARRAY_SIZE],  
               PriceIndArray[ARRAY_SIZE];  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray));  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray));  
memset(PriceIndArray, 0, sizeof(PriceIndArray));  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, SQL_PARAM_BIND_BY_COLUMN, 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in column-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  PartIDArray, 0, PartIDIndArray);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  DescArray, DESC_LEN, DescLenOrIndArray);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  PriceArray, 0, PriceIndArray);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartIDArray[i], DescArray[i], &PriceArray[i]);  
   PartIDIndArray[i] = 0;  
   DescLenOrIndArray[i] = SQL_NTS;  
   PriceIndArray[i] = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
}  
```  
  
## <a name="row-wise-binding"></a>El enlace  
 Cuando se usa el enlace, una aplicación define una estructura de cada conjunto de parámetros. La estructura contiene uno o dos elementos para cada parámetro. El primer elemento contiene el valor del parámetro y el segundo elemento contiene el búfer de longitud/indicador. La aplicación, a continuación, asigna una matriz de estas estructuras, que incluye tantos elementos como hay valores para cada parámetro.  
  
 La aplicación declara el tamaño de la estructura en el controlador con el atributo de instrucción SQL_ATTR_PARAM_BIND_TYPE. La aplicación enlaza las direcciones de los parámetros en la primera estructura de la matriz. Por lo tanto, el controlador puede calcular la dirección de los datos para una determinada fila y columna como  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 donde las filas se numeran del 1 al tamaño del conjunto de parámetros. El desplazamiento, si ha definido, es el valor señalado por el atributo de instrucción SQL_ATTR_PARAM_BIND_OFFSET_PTR. La siguiente ilustración muestra el modo de fila cómo funciona el enlace. Los parámetros se pueden colocar en la estructura en cualquier orden, pero se muestran en orden secuencial para mayor claridad.  
  
 ![Muestra cómo fila&#45;inteligente enlace funciona](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 El código siguiente crea una estructura con elementos para los valores que se va a almacenar en las columnas PartID, descripción y precio. A continuación, asigna una matriz de 10 elementos de estas estructuras y lo enlaza a los parámetros para las columnas PartID, descripción y precio, mediante el enlace. A continuación, ejecuta una instrucción para insertar 10 filas.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
typedef tagPartStruct {  
   SQLREAL       Price;  
   SQLUINTEGER   PartID;  
   SQLCHAR       Desc[DESC_LEN];  
   SQLINTEGER    PriceInd;  
   SQLINTEGER    PartIDInd;  
   SQLINTEGER    DescLenOrInd;  
} PartStruct;  
  
PartStruct PartArray[ARRAY_SIZE];  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  
                Price) "  
               "VALUES (?, ?, ?)";  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, sizeof(PartStruct), 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in row-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartArray[0].PartID, 0, &PartArray[0].PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  PartArray[0].Desc, DESC_LEN, &PartArray[0].DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &PartArray[0].Price, 0, &PartArray[0].PriceInd);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartArray[i].PartID, PartArray[i].Desc, &PartArray[i].Price);  
   PartArray[0].PartIDInd = 0;  
   PartArray[0].DescLenOrInd = SQL_NTS;  
   PartArray[0].PriceInd = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
```
