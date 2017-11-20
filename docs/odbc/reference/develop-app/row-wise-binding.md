---
title: El enlace | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4f622cf4-0603-47a1-a48b-944c4ef46364
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 967d7682c666dd6c413d49e083affeb55721742d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="row-wise-binding"></a>El enlace
Cuando se usa el enlace, una aplicación define una estructura que contiene uno o dos o, en algunos casos, tres, los elementos de cada columna para la que se devolverán datos. El primer elemento contiene el valor de datos y el segundo elemento contiene el búfer de longitud/indicador. Indicadores y los valores de longitud pueden almacenarse en búferes independientes al establecer los campos de descriptor SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR en valores diferentes; Si es así, la estructura contiene un tercer elemento. La aplicación, a continuación, asigne una matriz de estas estructuras, que contiene tantos elementos como filas en el conjunto de filas.  
  
 La aplicación declara el tamaño de la estructura en el controlador con el atributo de instrucción SQL_ATTR_ROW_BIND_TYPE y enlaza la dirección de cada miembro en el primer elemento de la matriz. Por lo tanto, el controlador puede calcular la dirección de los datos para una determinada fila y columna como  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 donde las filas se numeran del 1 al tamaño del conjunto de filas. (Uno se resta el número de fila porque está basado en cero en C la indización de matrices.) La ilustración siguiente muestra cómo funciona el enlace. Por lo general, solo las columnas que se enlazarán se incluyen en la estructura. La estructura puede contener campos que no estén relacionados como resultado columnas del conjunto. Las columnas se pueden colocar en la estructura en cualquier orden, pero se muestran en orden secuencial para mayor claridad.  
  
 ![Fila muestra &#45; enlace conveniente](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 Por ejemplo, el código siguiente crea una estructura con elementos en la que se va a devolver datos de las columnas OrderID y vendedor, estado y longitud/indicadores para las columnas vendedor y estado. Asigna 10 de estas estructuras y enlazarlas a las columnas OrderID, vendedor y estado.  
  
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

