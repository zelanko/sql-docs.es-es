---
title: Estado de actualización y eliminación posicionados de la sección de estado de la sección de actualizaciones y eliminación de la sección de Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e5316bee7057b30eace326b3ca82b30b75741fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282366"
---
# <a name="positioned-update-and-delete-statements"></a>Actualización posicionada y las instrucciones Delete
Las aplicaciones pueden actualizar o eliminar la fila actual de un conjunto de resultados con una instrucción de actualización o eliminación posicionada. Algunos orígenes de datos admiten instrucciones de actualización y eliminación posicionadas, pero no todas. Para determinar si un origen de datos admite instrucciones de actualización y eliminación posicionadas, una aplicación llama a **SQLGetInfo** con el SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 *InfoType* (según el tipo del cursor). Tenga en cuenta que la biblioteca de cursores ODBC simula instrucciones de actualización y eliminación posicionadas.  
  
 Para utilizar una instrucción de actualización o eliminación posicionada, la aplicación debe crear un conjunto de resultados con una instrucción **SELECT FOR UPDATE.** La sintaxis de esta instrucción es:  
  
 **SELECT** [**ALL** &#124; **DISTINCT**] *select-list*  
  
 **FROM** *tabla-referencia-lista*  
  
 [**DONDE estado** *de búsqueda*]  
  
 **PARA ACTUALIZAR** [*nombre-columna* [**,** *nombre-columna*]...]  
  
 A continuación, la aplicación coloca el cursor en la fila que se va a actualizar o eliminar. Puede hacerlo llamando a **SQLFetchScroll** para recuperar un conjunto de filas que contiene la fila necesaria y llamar a **SQLSetPos** para colocar el cursor del conjunto de filas en esa fila. A continuación, la aplicación ejecuta la instrucción update o delete posicionada en una instrucción diferente a la instrucción que utiliza el conjunto de resultados. La sintaxis de estas sentencias es:  
  
 **ACTUALIZAR** *nombre-tabla*  
  
 **SET** *column-identifier* **=** -*expresión* &#124; **NULL**?  
  
 [**,** *identificador de columna* **=** ,*expresión* &#124; **NULL]...**  
  
 **DONDE ACTUAL DE nombre-cursor** *cursor-name*  
  
 **DELETE FROM** *nombre-tabla* **WHERE CURRENT OF** *cursor-name*  
  
 Observe que estas instrucciones requieren un nombre de cursor. La aplicación puede especificar un nombre de cursor con **SQLSetCursorName** antes de ejecutar la instrucción que crea el conjunto de resultados o puede permitir que el origen de datos genere automáticamente un nombre de cursor cuando se crea el cursor. En este último caso, la aplicación recupera este nombre de cursor para su uso en instrucciones de actualización y eliminación posicionadas llamando a **SQLGetCursorName**.  
  
 Por ejemplo, el código siguiente permite a un usuario desplazarse por la tabla Customers y eliminar registros de clientes o actualizar sus direcciones y números de teléfono. Llama a **SQLSetCursorName** para especificar un nombre de cursor antes de crear el conjunto de resultados de los clientes y utiliza tres identificadores de instrucción: *hstmtCust* para el conjunto de resultados, *hstmtUpdate* para una instrucción de actualización posicionada y *hstmtDelete* para una instrucción delete posicionada. Aunque el código podría enlazar variables independientes a los parámetros de la instrucción update posicionada, actualiza los búferes del conjunto de filas y enlaza los elementos de estos búferes. Esto mantiene los búferes del conjunto de filas sincronizados con los datos actualizados.  
  
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
