---
title: SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a64b07754533a5916fbf3a4e860d9cbcfceee721
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419784"
---
# <a name="sqlgetdata"></a>SQLGetData
  **SQLGetData** se usa para recuperar datos del conjunto de resultados sin enlazar valores de columna. Se puede llamar sucesivamente a**SQLGetData** en la misma columna para recuperar cantidades grandes de datos de una columna con un tipo de datos **text**, **ntext**o **image** .  
  
 No es necesario que una aplicación enlace variables para capturar datos del conjunto de resultados. Se pueden recuperar los datos de cualquier columna de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client mediante el uso de **SQLGetData**.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no admite el uso **SQLGetData** para recuperar datos en orden aleatorio de columna. Todas las columnas sin enlazar procesadas con **SQLGetData** deben tener los ordinales de las columnas más altos que los de las columnas enlazadas en el conjunto de resultados. La aplicación debe procesar datos desde el valor ordinal de la columna sin enlazar más bajo hasta el valor más alto. Al intentar recuperar datos de una columna con un número ordinal más bajo, se genera un error. Si la aplicación está usando cursores de servidor para notificar las filas del conjunto de resultados, la aplicación puede intentar volver a capturar la fila actual y, a continuación, capturar el valor de una columna. Si una instrucción se ejecuta en el valor predeterminado de solo lectura, cursor de solo avance, se debe volver a ejecutar la instrucción para realizar un copia de seguridad de **SQLGetData**.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client notifica con precisión la longitud de **texto**, **ntext**, y **imagen** datos recuperados mediante **SQLGetData** . La aplicación puede hacer buen uso del parámetro *StrLen_or_IndPtr* devuelto para recuperar rápidamente los datos largos.  
  
> [!NOTE]  
>  Para tipos de valor grandes, *StrLen_or_IndPtr* devolverá SQL_NO_TOTAL en casos de truncamiento de datos.  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>SQLGetData admite las características mejoradas de fecha y hora  
 Los valores de columna de resultados de tipos de fecha y hora se convierten como se describe en [conversiones de SQL a C](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>SQLGetData admite UDT CLR grandes  
 **SQLGetData** admite los tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
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
 [Función SQLGetData](http://go.microsoft.com/fwlink/?LinkId=59350)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
