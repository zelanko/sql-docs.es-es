---
title: Usar SQLBindCol | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294635"
---
# <a name="using-sqlbindcol"></a>Uso de SQLBindCol
La aplicación enlaza las columnas llamando a **SQLBindCol**. Esta función enlaza una columna cada vez. Con él, la aplicación especifica lo siguiente:  
  
-   Número de columna. La columna 0 es la columna de marcador; Esta columna no se incluye en algunos conjuntos de resultados. Todas las demás columnas se numeran a partir del número 1. Es un error enlazar una columna con un número superior que contiene columnas en el conjunto de resultados. Este error no se puede detectar hasta que se haya creado el conjunto de resultados, por lo que se devuelve por **SQLFetch**, no **SQLBindCol**.  
  
-   El tipo de datos de C, la dirección y la longitud de bytes de la variable enlazada a la columna. Es un error especificar un tipo de datos de C al que no se puede convertir el tipo de datos SQL de la columna; es posible que este error no se detecte hasta que se haya creado el conjunto de resultados, por lo que se devuelve por **SQLFetch**, no **SQLBindCol**. Para obtener una lista de las conversiones admitidas, vea [convertir datos de SQL a tipos de datos de C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en el Apéndice D: tipos de datos. Para obtener información sobre la longitud de bytes, vea [longitud del búfer de datos](../../../odbc/reference/develop-app/data-buffer-length.md).  
  
-   Dirección de un búfer de longitud/indicador. El búfer de longitud/indicador es opcional. Se utiliza para devolver la longitud de bytes de los datos binarios o de caracteres, o para devolver SQL_NULL_DATA si los datos son NULL. Para obtener más información, vea [usar valores de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Cuando se llama a **SQLBindCol** , el controlador asocia esta información con la instrucción. Cuando se captura cada fila de datos, se usa la información para colocar los datos de cada columna en las variables de aplicación enlazadas.  
  
 Por ejemplo, el código siguiente enlaza las variables a las columnas SalesPerson y CustID. Los datos de las columnas se devolverán en *SalesPerson* y *CustID*. Dado que el *vendedor* es un búfer de caracteres, la aplicación especifica su longitud de bytes (11) para que el controlador pueda determinar si se truncan los datos. La longitud de bytes del título devuelto o si es NULL, se devolverá en *SalesPersonLenOrInd*.  
  
 Dado que *CustID* es una variable de tipo entero y tiene una longitud fija, no es necesario especificar su longitud de bytes; el controlador supone que es **sizeof (** sqluinteger que incluya **)**. La longitud de bytes de los datos devueltos del identificador de cliente, o si es NULL, se devolverá en *CustIDInd*. Tenga en cuenta que la aplicación solo está interesada en si el salario es NULL, ya que la longitud de bytes siempre es **sizeof (** sqluinteger que incluya **)**.  
  
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
  
 El código siguiente ejecuta una instrucción **Select** especificada por el usuario e imprime cada fila de datos en el conjunto de resultados. Dado que la aplicación no puede predecir la forma del conjunto de resultados creado por la instrucción **Select** , no puede enlazar variables codificadas de forma rígida al conjunto de resultados como en el ejemplo anterior. En su lugar, la aplicación asigna un búfer que contiene los datos y un búfer de longitud/indicador para cada columna de esa fila. Para cada columna, calcula el desplazamiento hasta el inicio de la memoria de la columna y ajusta este desplazamiento para que los datos y los búferes de indicador/longitud de la columna se inicien en los límites de alineación. A continuación, enlaza la memoria a partir de la posición de desplazamiento a la columna. Desde el punto de vista del controlador, la dirección de esta memoria no se distingue de la dirección de una variable enlazada en el ejemplo anterior. Para obtener más información sobre la alineación, vea [alignment](../../../odbc/reference/develop-app/alignment.md).  
  
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
