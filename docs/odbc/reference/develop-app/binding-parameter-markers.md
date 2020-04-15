---
title: Marcadores de parámetros de enlace ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be99bc884a8baa66f3d632ee4731985f0cc85732
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306396"
---
# <a name="binding-parameter-markers"></a>Marcadores de parámetros de enlace
La aplicación enlaza parámetros llamando a **SQLBindParameter**. **SQLBindParameter** enlaza un parámetro a la vez. Con él, la aplicación especifica lo siguiente:  
  
-   El número de parámetro. Los parámetros se numeran en orden de parámetros crecientes en la instrucción SQL, empezando por el número 1. Aunque es legal especificar un número de parámetro que sea mayor que el número de parámetros de la instrucción SQL, el valor del parámetro se omitirá cuando se ejecute la instrucción.  
  
-   El tipo de parámetro (entrada, entrada/salida o salida). Excepto los parámetros en las llamadas a procedimientos, todos los parámetros son parámetros de entrada. Para obtener más información, consulte [Parámetros](../../../odbc/reference/develop-app/procedure-parameters.md)de procedimiento , más adelante en esta sección.  
  
-   El tipo de datos C, la dirección y la longitud de bytes de la variable enlazada al parámetro. El controlador debe ser capaz de convertir los datos del tipo de datos C al tipo de datos SQL o se devuelve un error. Para obtener una lista de las conversiones admitidas, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) de datos SQL en Apéndice D: tipos de datos.  
  
-   El tipo de datos SQL, la precisión y la escala del propio parámetro.  
  
-   La dirección de un búfer de longitud/indicador. Proporciona la longitud de bytes de datos binarios o de caracteres, especifica que los datos son NULL o especifica que los datos se enviarán con **SQLPutData**. Para obtener más información, consulte Uso de valores de [longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Por ejemplo, el código siguiente enlaza *SalesPerson* y *CustID* a los parámetros de las columnas SalesPerson y CustID. Dado que *SalesPerson* contiene datos de caracteres, que son de longitud variable, el código especifica la longitud de bytes de *SalesPerson* (11) y enlaza *SalesPersonLenOrInd* para que contenga la longitud de bytes de los datos en *SalesPerson*. Esta información no es necesaria para *CustID* porque contiene datos enteros, que son de longitud fija.  
  
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
  
 Cuando **SQLBindParameter** se llama, el controlador almacena esta información en la estructura de la instrucción. Cuando se ejecuta la instrucción, utiliza la información para recuperar los datos del parámetro y enviarlos al origen de datos.  
  
> [!NOTE]  
>  En ODBC 1.0, los parámetros se enlazaban con **SQLSetParam**. El Administrador de controladores asigna llamadas entre **SQLSetParam** y **SQLBindParameter**, dependiendo de las versiones de ODBC utilizadas por la aplicación y el controlador.
