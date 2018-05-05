---
title: Coloca las instrucciones Update y Delete | Documentos de Microsoft
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
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1f01ea9009e516d3962c1fbb175dff4f90f5d10
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="positioned-update-and-delete-statements"></a>Actualización posicionada y las instrucciones Delete
Las aplicaciones pueden actualizar o eliminar la fila actual de un conjunto de resultados con una actualización por posición o la instrucción delete. Coloca update y delete instrucciones son compatibles con algunos orígenes de datos, pero no todas ellas. Para determinar si un origen de datos admite coloca instrucciones update y delete, llama a una aplicación **SQLGetInfo** con el SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 *tipo de información* (según el tipo del cursor). Tenga en cuenta que la biblioteca de cursores ODBC simula coloca instrucciones update y delete.  
  
 Para utilizar una actualización por posición o la instrucción delete, la aplicación debe crear un conjunto de resultados con un **seleccione para actualizar** instrucción. La sintaxis de esta instrucción es:  
  
 **Seleccione** [**todos los** &#124; **DISTINCT**] *lista de selección*  
  
 **DE** *lista de referencias de tabla*  
  
 [**Donde** *condición de búsqueda*]  
  
 **PARA la actualización de** [*nombre de la columna* [**,** *nombre de la columna*]...]  
  
 La aplicación, a continuación, coloca el cursor en la fila para actualizarse o eliminarse. Puede hacerlo mediante una llamada a **SQLFetchScroll** para recuperar un conjunto de filas que contiene la fila necesaria y llamar a **SQLSetPos** para colocar el cursor de conjunto de filas en esa fila. A continuación, la aplicación ejecuta la instrucción de eliminación o actualización posicionada en una instrucción diferente que la instrucción que se va a utilizar el conjunto de resultados. Es la sintaxis de estas instrucciones:  
  
 **ACTUALIZACIÓN** *nombre de la tabla*  
  
 **ESTABLECER** *identificador de la columna* **=** {*expresión* &#124; **NULL**}  
  
 [**,** *identificador de la columna* **=** {*expresión* &#124; **NULL**}]...  
  
 **WHERE CURRENT OF** *nombre del cursor*  
  
 **DELETE FROM** *nombre de la tabla* **WHERE CURRENT OF** *nombre del cursor*  
  
 Tenga en cuenta que estas instrucciones requieren un nombre de cursor. La aplicación puede especificar un nombre de cursor con **SQLSetCursorName** antes de ejecutar la instrucción que crea el resultado de establece o puede dejar que el origen de datos automáticamente, generar un nombre de cursor cuando se crea el cursor. En el último caso, la aplicación recupera este nombre de cursor para su uso en instrucciones de eliminación y actualización posicionada mediante una llamada a **SQLGetCursorName**.  
  
 Por ejemplo, el código siguiente permite a un usuario a desplazarse por la tabla Customers y eliminar los registros de clientes o actualizar las direcciones y números de teléfono. Llama **SQLSetCursorName** para especificar un nombre de cursor antes de que se crea el conjunto de resultados de clientes y utiliza tres identificadores de instrucciones: *hstmtCust* para el conjunto de resultados, *hstmtUpdate* en una instrucción de actualización por posición, y *hstmtDelete* para una posición la instrucción delete. Aunque el código podría enlazar variables independientes para los parámetros de la instrucción de actualización posicionada, actualiza los búferes de conjunto de filas y enlaza los elementos de estos búferes. Esto evita que los búferes de conjunto de filas sincronizados con los datos actualizados.  
  
```  
#define POSITIONED_UPDATE 100  
#define POSITIONED_DELETE 101  
  
SQLUINTEGER    CustIDArray[10];  
SQLCHAR        NameArray[10][51], AddressArray[10][51],   
               PhoneArray[10][11];  
SQLINTEGER     CustIDIndArray[10], NameLenOrIndArray[10],   
               AddressLenOrIndArray[10],  
               PhoneLenOrIndArray[10];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLHSTMT       hstmtCust, hstmtUpdate, hstmtDelete;  
  
// Set the SQL_ATTR_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmtCust, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmtCust, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]),  
            NameLenOrIndArray);  
SQLBindCol(hstmtCust, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
         AddressLenOrIndArray);  
SQLBindCol(hstmtCust, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Set the cursor name to Cust.  
SQLSetCursorName(hstmtCust, "Cust", SQL_NTS);  
  
// Prepare positioned update and delete statements.  
SQLPrepare(hstmtUpdate,  
   "UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust",  
   SQL_NTS);  
SQLPrepare(hstmtDelete, "DELETE FROM Customers WHERE CURRENT OF Cust", SQL_NTS);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmtCust,  
   "SELECT CustID, Name, Address, Phone FROM Customers FOR UPDATE OF Address, Phone",  
   SQL_NTS);  
  
// Fetch and display the first 10 rows.  
SQLFetchScroll(hstmtCust, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmtCust, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray, PhoneArray,  
                     PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case POSITIONED_UPDATE:  
         // Get the new data and place it in the rowset buffers.  
         GetNewData(AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                     PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Bind the elements of the arrays at position RowNum-1 to the   
         // parameters of the positioned update statement.  
         SQLBindParameter(hstmtUpdate, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           50, 0, AddressArray[RowNum - 1], sizeof(AddressArray[0]),  
                           &AddressLenOrIndArray[RowNum - 1]);  
         SQLBindParameter(hstmtUpdate, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           10, 0, PhoneArray[RowNum - 1], sizeof(PhoneArray[0]),  
                           &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned update statement to update the row.  
         SQLExecute(hstmtUpdate);  
         break;  
  
      case POSITIONED_DELETE:  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned delete statement to delete the row.  
         SQLExecute(hstmtDelete);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmtCust);  
```
