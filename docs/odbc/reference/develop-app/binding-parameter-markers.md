---
title: Marcadores de parámetros de enlace | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e625e01b9bf4771f18dd8e9807ab09100ca580c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107648"
---
# <a name="binding-parameter-markers"></a>Marcadores de parámetros de enlace
La aplicación enlaza los parámetros llamando a **SQLBindParameter**. **SQLBindParameter** enlaza un parámetro cada vez. Con él, la aplicación especifica lo siguiente:  
  
-   El número de parámetro. Los parámetros se numeran al aumentar el orden de los parámetros en la instrucción SQL, empezando por el número 1. Aunque es válido especificar un número de parámetro mayor que el número de parámetros de la instrucción SQL, se omitirá el valor del parámetro cuando se ejecute la instrucción.  
  
-   El tipo de parámetro (entrada, entrada/salida o salida). A excepción de los parámetros de las llamadas a procedimientos, todos los parámetros son parámetros de entrada. Para obtener más información, vea [parámetros de procedimientos](../../../odbc/reference/develop-app/procedure-parameters.md), más adelante en esta sección.  
  
-   El tipo de datos de C, la dirección y la longitud de bytes de la variable enlazada al parámetro. El controlador debe ser capaz de convertir los datos del tipo de datos C al tipo de datos SQL o se devuelve un error. Para obtener una lista de las conversiones admitidas, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) en el Apéndice D: tipos de datos.  
  
-   El tipo de datos SQL, la precisión y la escala del propio parámetro.  
  
-   Dirección de un búfer de longitud/indicador. Proporciona la longitud de bytes de los datos binarios o de caracteres, especifica que los datos son NULL o especifica que los datos se enviarán con **SQLPutData**. Para obtener más información, vea [usar valores de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Por ejemplo, el código siguiente enlaza *SalesPerson* y *CustID* a los parámetros de las columnas Salesperson y CustID. Dado que el *vendedor* contiene datos de caracteres, que son de longitud variable, el código especifica la longitud en bytes del *vendedor* (11) y enlaza *SalesPersonLenOrInd* para que contenga la longitud de bytes de los datos del *vendedor*. Esta información no es necesaria para *CustID* porque contiene datos enteros, que es de longitud fija.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 Cuando se llama a **SQLBindParameter** , el controlador almacena esta información en la estructura de la instrucción. Cuando se ejecuta la instrucción, se usa la información para recuperar los datos del parámetro y enviarlos al origen de datos.  
  
> [!NOTE]  
>  En ODBC 1,0, los parámetros estaban enlazados con **SQLSetParam**. El administrador de controladores asigna llamadas entre **SQLSetParam** y **SQLBindParameter**, en función de las versiones de ODBC que usa la aplicación y el controlador.
