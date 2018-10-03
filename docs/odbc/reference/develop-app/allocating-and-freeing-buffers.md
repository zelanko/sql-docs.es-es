---
title: Asignar y liberar búferes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 388147de8935d36180ba9845c8353bbf3dd6edc0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682833"
---
# <a name="allocating-and-freeing-buffers"></a>Asignar y liberar búferes
Todos los búferes se asigna y libera la aplicación. Si no se aplaza un búfer, sólo debe existir para el tiempo que dure la llamada a una función. Por ejemplo, **SQLGetInfo** devuelve el valor asociado con una opción concreta en el búfer señalado por el *InfoValuePtr* argumento. Este búfer se puede liberar inmediatamente después de llamar a **SQLGetInfo**, tal y como se muestra en el ejemplo de código siguiente:  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 Dado que búferes diferidos se especifica en una función y se usa en otro, es un error de programación de aplicaciones para liberar un búfer aplazado mientras el controlador todavía espera que exista. Por ejemplo, la dirección de la \* *ValuePtr* búfer se pasa a **SQLBindCol** para su uso posterior por **SQLFetch**. Este búfer no se podrá liberar hasta que la columna es independiente, como con una llamada a **SQLBindCol** o **SQLFreeStmt** tal como se muestra en el ejemplo de código siguiente:  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 Este error se realiza fácilmente declarando el búfer de forma local en una función; el búfer se libera cuando la aplicación sale la función. Por ejemplo, el siguiente código, comportamiento no definido y probablemente irrecuperable en el controlador:  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```
