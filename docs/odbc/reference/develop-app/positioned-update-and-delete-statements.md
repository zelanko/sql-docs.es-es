---
title: Instrucciones Update y DELETE posicionadas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b37bdfae5f97a453477768aca39b801c06c0701
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023295"
---
# <a name="positioned-update-and-delete-statements"></a>Actualización posicionada y las instrucciones Delete
Las aplicaciones pueden actualizar o eliminar la fila actual de un conjunto de resultados con una instrucción UPDATE o DELETE posicionada. Algunos orígenes de datos admiten las instrucciones Update y DELETE posicionadas, pero no todas ellas. Para determinar si un origen de datos admite instrucciones Update y DELETE posicionadas, una aplicación llama a **SQLGetInfo** con el SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 *InfoType* (dependiendo del tipo de cursor). Tenga en cuenta que la biblioteca de cursores ODBC simula las instrucciones Update y DELETE posicionadas.  
  
 Para usar una instrucción UPDATE o DELETE posicionada, la aplicación debe crear un conjunto de resultados con una instrucción **Select for update** . La sintaxis de esta instrucción es:  
  
 **Select** [**All** &#124; **DISTINCT**] *Select-List*  
  
 **Desde** *la lista de referencias de tabla*  
  
 [**Where** *-condición de búsqueda*]  
  
 **Para la actualización de** [*nombre-columna* [**,** *nombre-columna*]...]  
  
 A continuación, la aplicación coloca el cursor en la fila que se va a actualizar o eliminar. Para ello, puede llamar a **SQLFetchScroll** para recuperar un conjunto de filas que contenga la fila requerida y llamar a **SQLSetPos** para colocar el cursor de conjunto de filas en esa fila. A continuación, la aplicación ejecuta la instrucción UPDATE o DELETE posicionada en una instrucción diferente de la instrucción que utiliza el conjunto de resultados. La sintaxis de estas instrucciones es:  
  
 **Actualizar** *tabla-nombre*  
  
 **Establecer** *el identificador de columna* **=** {*expresión* &#124; **null**}  
  
 [**,** *identificador de columna* **=** {*expresión* &#124; **null**}]...  
  
 **WHERE CURRENT of** *cursor-Name*  
  
 **Eliminar de** *TABLE-Name* **donde Current of** *cursor-Name*  
  
 Tenga en cuenta que estas instrucciones requieren un nombre de cursor. La aplicación puede especificar un nombre de cursor con **SQLSetCursorName** antes de ejecutar la instrucción que crea el conjunto de resultados, o puede permitir que el origen de datos genere automáticamente un nombre de cursor cuando se crea el cursor. En el último caso, la aplicación recupera este nombre de cursor para usarlo en las instrucciones Update y DELETE posicionadas mediante una llamada a **SQLGetCursorName**.  
  
 Por ejemplo, el código siguiente permite al usuario desplazarse por la tabla Customers y eliminar registros de cliente o actualizar sus direcciones y números de teléfono. Llama a **SQLSetCursorName** para especificar un nombre de cursor antes de crear el conjunto de resultados de los clientes y utiliza tres identificadores de instrucciones: *hstmtCust* para el conjunto de resultados, *hstmtUpdate* para una instrucción UPDATE posicionada y *hstmtDelete* para una instrucción Delete posicionada. Aunque el código podría enlazar variables independientes a los parámetros de la instrucción UPDATE posicionada, actualiza los búferes del conjunto de filas y enlaza los elementos de estos búferes. Esto mantiene los búferes del conjunto de filas sincronizados con los datos actualizados.  
  
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
