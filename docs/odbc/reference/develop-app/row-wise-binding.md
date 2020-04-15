---
title: Encuadernación de fila y sabiduría ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4f622cf4-0603-47a1-a48b-944c4ef46364
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a63565590bbafc6f3a8740dd7cf7d4acbfd4f80
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304276"
---
# <a name="row-wise-binding"></a>El enlace
Cuando se usa el enlace de fila, una aplicación define una estructura que contiene uno o dos, o en algunos casos tres, elementos para cada columna para la que se van a devolver los datos. El primer elemento contiene el valor de datos y el segundo elemento contiene el búfer de longitud/indicador. Los indicadores y los valores de longitud se pueden almacenar en búferes independientes estableciendo los campos SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR descriptor en valores diferentes; si esto se hace, la estructura contiene un tercer elemento. A continuación, la aplicación asigna una matriz de estas estructuras, que contiene tantos elementos como filas en el conjunto de filas.  
  
 La aplicación declara el tamaño de la estructura para el controlador con el atributo de instrucción SQL_ATTR_ROW_BIND_TYPE y enlaza la dirección de cada miembro en el primer elemento de la matriz. Por lo tanto, el controlador puede calcular la dirección de los datos para una fila y columna determinada como  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 donde las filas se numeran de 1 al tamaño del conjunto de filas. (Uno se resta del número de fila porque la indexación de matrices en C se basa en cero.) En la siguiente ilustración se muestra cómo funciona el enlace de fila. Por lo general, solo las columnas que se enlazarán se incluyen en la estructura. La estructura puede contener campos que no están relacionados con las columnas del conjunto de resultados. Las columnas se pueden colocar en la estructura en cualquier orden, pero se muestran en orden secuencial para mayor claridad.  
  
 ![Muestra la fila&#45;encuadernación sabia](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 Por ejemplo, el código siguiente crea una estructura con elementos en los que devolver datos para las columnas OrderID, SalesPerson y Status, y longitud/indicadores para las columnas SalesPerson y Status. Asigna 10 de estas estructuras y las enlaza a las columnas OrderID, SalesPerson y Status.  
  
```  
#define ROW_ARRAY_SIZE 10  
  
// Define the ORDERINFO struct and allocate an array of 10 structs.  
typedef struct {  
   SQLUINTEGER   OrderID;  
   SQLINTEGER    OrderIDInd;  
   SQLCHAR       SalesPerson[11];  
   SQLINTEGER    SalesPersonLenOrInd;  
   SQLCHAR       Status[7];  
   SQLINTEGER    StatusLenOrInd;  
} ORDERINFO;  
ORDERINFO OrderInfoArray[ROW_ARRAY_SIZE];  
  
SQLULEN    NumRowsFetched;  
SQLUSMALLINT   RowStatusArray[ROW_ARRAY_SIZE], i;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Specify the size of the structure with the SQL_ATTR_ROW_BIND_TYPE  
// statement attribute. This also declares that row-wise binding will  
// be used. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE  
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement  
// attribute to point to the row status array. Set the  
// SQL_ATTR_ROWS_FETCHED_PTR statement attribute to point to  
// NumRowsFetched.  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, sizeof(ORDERINFO), 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, ROW_ARRAY_SIZE, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROWS_FETCHED_PTR, &NumRowsFetched, 0);  
  
// Bind elements of the first structure in the array to the OrderID,  
// SalesPerson, and Status columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &OrderInfoArray[0].OrderID, 0, &OrderInfoArray[0].OrderIDInd);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, OrderInfoArray[0].SalesPerson,  
            sizeof(OrderInfoArray[0].SalesPerson),  
            &OrderInfoArray[0].SalesPersonLenOrInd);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, OrderInfoArray[0].Status,  
            sizeof(OrderInfoArray[0].Status), &OrderInfoArray[0].StatusLenOrInd);  
  
// Execute a statement to retrieve rows from the Orders table.  
SQLExecDirect(hstmt, "SELECT OrderID, SalesPerson, Status FROM Orders", SQL_NTS);  
  
// Fetch up to the rowset size number of rows at a time. Print the actual  
// number of rows fetched; this number is returned in NumRowsFetched.  
// Check the row status array to print only those rows successfully  
// fetched. Code to check if rc equals SQL_SUCCESS_WITH_INFO or  
// SQL_ERRORnot shown.  
while ((rc = SQLFetchScroll(hstmt,SQL_FETCH_NEXT,0)) != SQL_NO_DATA) {  
   for (i = 0; i < NumRowsFetched; i++) {  
      if (RowStatusArray[i] == SQL_ROW_SUCCESS|| RowStatusArray[i] ==   
         SQL_ROW_SUCCESS_WITH_INFO) {  
         if (OrderInfoArray[i].OrderIDInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%d\t", OrderInfoArray[i].OrderID);  
         if (OrderInfoArray[i].SalesPersonLenOrInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%s\t", OrderInfoArray[i].SalesPerson);  
         if (OrderInfoArray[i].StatusLenOrInd == SQL_NULL_DATA)  
            printf(" NULL\n");  
         else  
            printf("%s\n", OrderInfoArray[i].Status);  
      }  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
