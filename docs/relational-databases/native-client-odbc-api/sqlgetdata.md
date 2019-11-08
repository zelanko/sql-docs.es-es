---
title: SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 27b8fe304f26c60697e5d6fb147be20e30c86094
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786540"
---
# <a name="sqlgetdata"></a>SQLGetData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLGetData** se usa para recuperar datos del conjunto de resultados sin enlazar valores de columna. Se puede llamar sucesivamente a**SQLGetData** en la misma columna para recuperar cantidades grandes de datos de una columna con un tipo de datos **text**, **ntext**o **image** .  
  
 No es necesario que una aplicación enlace variables para capturar datos del conjunto de resultados. Los datos de cualquier columna se pueden recuperar del controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mediante **SQLGetData**.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no permite usar **SQLGetData** para recuperar datos en orden aleatorio de columna. Todas las columnas sin enlazar procesadas con **SQLGetData** deben tener los ordinales de las columnas más altos que los de las columnas enlazadas en el conjunto de resultados. La aplicación debe procesar datos desde el valor ordinal de la columna sin enlazar más bajo hasta el valor más alto. Al intentar recuperar datos de una columna con un número ordinal más bajo, se genera un error. Si la aplicación está usando cursores de servidor para notificar las filas del conjunto de resultados, la aplicación puede intentar volver a capturar la fila actual y, a continuación, capturar el valor de una columna. Si una instrucción se ejecuta en el valor predeterminado de solo lectura, cursor de solo avance, se debe volver a ejecutar la instrucción para realizar un copia de seguridad de **SQLGetData**.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client notifica con precisión la longitud de los datos recuperados **text**, **ntext**e **image** mediante **SQLGetData**. La aplicación puede hacer buen uso del parámetro *StrLen_or_IndPtr* devuelto para recuperar rápidamente los datos largos.  
  
> [!NOTE]  
>  Para tipos de valor grandes, *StrLen_or_IndPtr* devolverá SQL_NO_TOTAL en casos de truncamiento de datos.  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>SQLGetData admite las características mejoradas de fecha y hora  
 Los valores de las columnas de resultados de los tipos de fecha y hora se convierten como se describe en [conversiones de SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Para obtener más información, vea [mejoras &#40;de fecha y&#41;hora ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>SQLGetData admite UDT CLR grandes  
 **SQLGetData** admite los tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [ &#40;tipos CLR grandes definidos por el&#41;usuario ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="example"></a>Ejemplo  
  
```  
SQLHDBC     hDbc = NULL;  
SQLHSTMT    hStmt = NULL;  
long        lEmpID;  
PBYTE       pPicture;  
SQLINTEGER  pIndicators[2];  
  
// Get an environment, connection, and so on.  
...  
  
// Get a statement handle and execute a command.  
SQLAllocHandle(SQL_HANDLE_STMT, hDbc, &hStmt);  
  
if (SQLExecDirect(hStmt,  
    (SQLCHAR*) "SELECT EmployeeID, Photo FROM Employees",  
    SQL_NTS) == SQL_ERROR)  
    {  
    // Handle error and return.  
    }  
  
// Retrieve data from row set.  
SQLBindCol(hStmt, 1, SQL_C_LONG, (SQLPOINTER) &lEmpID, sizeof(long),  
    &pIndicators[0]);  
  
while (SQLFetch(hStmt) == SQL_SUCCESS)  
    {  
    cout << "EmployeeID: " << lEmpID << "\n";  
  
    // Call SQLGetData to determine the amount of data that's waiting.  
    if (SQLGetData(hStmt, 2, SQL_C_BINARY, pPicture, 0, &pIndicators[1])  
        == SQL_SUCCESS_WITH_INFO)  
        {  
        cout << "Photo size: " pIndicators[1] << "\n\n";  
  
        // Get all the data at once.  
        pPicture = new BYTE[pIndicators[1]];  
        if (SQLGetData(hStmt, 2, SQL_C_DEFAULT, pPicture,  
            pIndicators[1], &pIndicators[1]) != SQL_SUCCESS)  
            {  
            // Handle error and continue.  
            }  
  
        delete [] pPicture;  
        }  
    else  
        {  
        // Handle error on attempt to get data length.  
        }  
    }  
```  
  
## <a name="see-also"></a>Vea también  
 [SQLGetData (función](https://go.microsoft.com/fwlink/?LinkId=59350) )   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
