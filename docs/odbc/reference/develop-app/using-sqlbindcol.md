---
title: Uso de SQLBindCol ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
- SQLBindCol function [ODBC], using
ms.assetid: 17277ab3-33ad-44d3-a81c-a26b5e338512
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da49ad4db80b93d02534a0c4ecacdc2621c9cf8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294635"
---
# <a name="using-sqlbindcol"></a>Uso de SQLBindCol
La aplicación enlaza columnas llamando a **SQLBindCol**. Esta función enlaza una columna a la vez. Con él, la aplicación especifica lo siguiente:  
  
-   Número de columna. Columna 0 es la columna de marcador; esta columna no se incluye en algunos conjuntos de resultados. Todas las demás columnas se numeran a partir del número 1. Es un error enlazar una columna con mayor número que las columnas del conjunto de resultados; Este error no se puede detectar hasta que se haya creado el conjunto de resultados, por lo que SQLFetch lo **devuelve,** no **SQLBindCol**.  
  
-   El tipo de datos C, la dirección y la longitud de bytes de la variable enlazada a la columna. Es un error especificar un tipo de datos C al que no se puede convertir el tipo de datos SQL de la columna; Es posible que este error no se detecte hasta que se haya creado el conjunto de resultados, por lo que SQLFetch lo **devuelve,** no **SQLBindCol**. Para obtener una lista de las conversiones admitidas, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) de datos C en Apéndice D: tipos de datos. Para obtener información sobre la longitud del byte, vea [Longitud del búfer](../../../odbc/reference/develop-app/data-buffer-length.md)de datos .  
  
-   La dirección de un búfer de longitud/indicador. El búfer de longitud/indicador es opcional. Se utiliza para devolver la longitud de bytes de datos binarios o de caracteres o devolver SQL_NULL_DATA si los datos son NULL. Para obtener más información, consulte Uso de valores de [longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Cuando **SQLBindCol** se llama, el controlador asocia esta información con la instrucción. Cuando se recupera cada fila de datos, utiliza la información para colocar los datos de cada columna en las variables de aplicación enlazadas.  
  
 Por ejemplo, el código siguiente enlaza variables a las columnas SalesPerson y CustID. Los datos de las columnas se devolverán en *SalesPerson* y *CustID*. Dado que *SalesPerson* es un búfer de caracteres, la aplicación especifica su longitud de bytes (11) para que el controlador pueda determinar si se truncan los datos. La longitud de bytes del título devuelto, o si es NULL, se devolverá en *SalesPersonLenOrInd*.  
  
 Dado que *CustID* es una variable entera y tiene longitud fija, no es necesario especificar su longitud de byte; el controlador asume que es **sizeof(** SQLUINTEGER **)**. La longitud de bytes de los datos de identificador de cliente devueltos, o si es NULL, se devolverá en *CustIDInd*. Tenga en cuenta que la aplicación solo está interesada en si el salario es NULL, porque la longitud del byte siempre es **sizeof(** SQLUINTEGER **)**.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLUINTEGER   CustID;  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLRETURN     rc;  
SQLHSTMT      hstmt;  
  
// Bind SalesPerson to the SalesPerson column and CustID to the   
// CustID column.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, SalesPerson, sizeof(SalesPerson),  
            &SalesPersonLenOrInd);  
SQLBindCol(hstmt, 2, SQL_C_ULONG, &CustID, 0, &CustIDInd);  
  
// Execute a statement to get the sales person/customer of all orders.  
SQLExecDirect(hstmt, "SELECT SalesPerson, CustID FROM Orders ORDER BY SalesPerson",  
               SQL_NTS);  
  
// Fetch and print the data. Print "NULL" if the data is NULL. Code to   
// check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (SalesPersonLenOrInd == SQL_NULL_DATA)   
            printf("NULL                     ");  
   else   
            printf("%10s   ", SalesPerson);  
   if (CustIDInd == SQL_NULL_DATA)   
         printf("NULL\n");  
   else   
            printf("%d\n", CustID);  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 El código siguiente ejecuta una instrucción **SELECT** introducida por el usuario e imprime cada fila de datos en el conjunto de resultados. Dado que la aplicación no puede predecir la forma del conjunto de resultados creado por la instrucción **SELECT,** no puede enlazar variables codificadas de forma rígida al conjunto de resultados como en el ejemplo anterior. En su lugar, la aplicación asigna un búfer que contiene los datos y un búfer de longitud/indicador para cada columna de esa fila. Para cada columna, calcula el desplazamiento al inicio de la memoria de la columna y ajusta este desplazamiento para que los datos y los búferes de longitud/indicador para la columna comiencen en los límites de alineación. A continuación, enlaza la memoria comenzando en el desplazamiento a la columna. Desde el punto de vista del controlador, la dirección de esta memoria es indistinguible de la dirección de una variable enlazada en el ejemplo anterior. Para obtener más información sobre la alineación, consulte [Alineación](../../../odbc/reference/develop-app/alignment.md).  
  
```  
// This application allocates a buffer at run time. For each column, this   
// buffer contains memory for the column's data and length/indicator.   
// For example:  
//      column 1         column 2      column 3      column 4  
// <------------><---------------><-----><------------>  
//      db1   li1   db2   li2   db3   li3   db4   li4  
//      |      |      |      |      |      |      |         |  
//      _____V_____V________V_______V___V___V______V_____V_  
// |__________|__|_____________|__|___|__|__________|__|  
//  
// dbn = data buffer for column n  
// lin = length/indicator buffer for column n  
  
// Define a macro to increase the size of a buffer so that it is a   
// multiple of the alignment size. Thus, if a buffer starts on an   
// alignment boundary, it will end just before the next alignment   
// boundary. In this example, an alignment size of 4 is used because   
// this is the size of the largest data type used in the application's   
// buffer--the size of an SDWORD and of the largest default C data type   
// are both 4. If a larger data type (such as _int64) was used, it would   
// be necessary to align for that size.  
#define ALIGNSIZE 4  
#define ALIGNBUF(Length) Length % ALIGNSIZE ? \  
                  Length + ALIGNSIZE - (Length % ALIGNSIZE) : Length  
  
SQLCHAR        SelectStmt[100];  
SQLSMALLINT    NumCols, *CTypeArray, i;  
SQLINTEGER *   ColLenArray, *OffsetArray, SQLType, *DataPtr;  
SQLRETURN      rc;   
SQLHSTMT       hstmt;  
  
// Get a SELECT statement from the user and execute it.  
GetSelectStmt(SelectStmt, 100);  
SQLExecDirect(hstmt, SelectStmt, SQL_NTS);  
  
// Determine the number of result set columns. Allocate arrays to hold   
// the C type, byte length, and buffer offset to the data.  
SQLNumResultCols(hstmt, &NumCols);  
CTypeArray = (SQLSMALLINT *) malloc(NumCols * sizeof(SQLSMALLINT));  
ColLenArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
OffsetArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
  
OffsetArray[0] = 0;  
for (i = 0; i < NumCols; i++) {  
   // Determine the column's SQL type. GetDefaultCType contains a switch   
   // statement that returns the default C type for each SQL type.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i) + 1, SQL_DESC_TYPE, NULL, 0, NULL, (SQLPOINTER) &SQLType);  
   CTypeArray[i] = GetDefaultCType(SQLType);  
  
   // Determine the column's byte length. Calculate the offset in the   
   // buffer to the data as the offset to the previous column, plus the   
   // byte length of the previous column, plus the byte length of the   
   // previous column's length/indicator buffer. Note that the byte   
   // length of the column and the length/indicator buffer are increased   
   // so that, assuming they start on an alignment boundary, they will  
   // end on the byte before the next alignment boundary. Although this   
   // might leave some holes in the buffer, it is a relatively   
   // inexpensive way to guarantee alignment.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i)+1, SQL_DESC_OCTET_LENGTH, NULL, 0, NULL, &ColLenArray[i]);  
   ColLenArray[i] = ALIGNBUF(ColLenArray[i]);  
   if (i)  
      OffsetArray[i] = OffsetArray[i-1]+ColLenArray[i-1]+ALIGNBUF(sizeof(SQLINTEGER));  
}  
  
// Allocate the data buffer. The size of the buffer is equal to the   
// offset to the data buffer for the final column, plus the byte length   
// of the data buffer and length/indicator buffer for the last column.  
void *DataPtr = malloc(OffsetArray[NumCols - 1] +  
               ColLenArray[NumCols - 1] + ALIGNBUF(sizeof(SQLINTEGER)));  
  
// For each column, bind the address in the buffer at the start of the   
// memory allocated for that column's data and the address at the start   
// of the memory allocated for that column's length/indicator buffer.  
for (i = 0; i < NumCols; i++)  
   SQLBindCol(hstmt,  
            ((SQLUSMALLINT) i) + 1,  
            CTypeArray[i],  
            (SQLPOINTER)((SQLCHAR *)DataPtr + OffsetArray[i]),  
            ColLenArray[i],  
            (SQLINTEGER *)((SQLCHAR *)DataPtr + OffsetArray[i] + ColLenArray[i]));  
  
// Retrieve and print each row. PrintData accepts a pointer to the data,   
// its C type, and its byte length/indicator. It contains a switch   
// statement that casts and prints the data according to its type. Code   
// to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   for (i = 0; i < NumCols; i++) {  
      PrintData((SQLCHAR *)DataPtr[OffsetArray[i]], CTypeArray[i],  
               (SQLINTEGER *)((SQLCHAR *)DataPtr[OffsetArray[i] + ColLenArray[i]]));  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
