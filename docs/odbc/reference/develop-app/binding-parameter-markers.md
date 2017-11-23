---
title: "Marcadores de parámetros de enlace | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea1c1ecd676c7a496f7856f0eb0b22b003183407
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="binding-parameter-markers"></a>Marcadores de parámetros de enlace
La aplicación enlaza los parámetros mediante una llamada a **SQLBindParameter**. **SQLBindParameter** enlaza un parámetro a la vez. Con él, la aplicación especifica lo siguiente:  
  
-   El número de parámetro. Parámetros se numeran en orden creciente de los parámetros en la instrucción SQL, comenzando por el número 1. Aunque es legal para especificar un número de parámetro que sea mayor que el número de parámetros en la instrucción SQL, se omitirá el valor del parámetro cuando se ejecuta la instrucción.  
  
-   El tipo de parámetro (entrada, entrada/salida o de salida). Salvo parámetros en las llamadas a procedimiento, todos los parámetros son parámetros de entrada. Para obtener más información, consulte [parámetros de procedimiento](../../../odbc/reference/develop-app/procedure-parameters.md), más adelante en esta sección.  
  
-   La longitud de bytes, la dirección y el tipo de datos de C de la variable enlazado al parámetro. El controlador debe ser capaz de convertir los datos del tipo de datos C en el tipo de datos SQL o se devuelve un error. Para obtener una lista de conversiones admitidas, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) en tipos de datos de apéndice D:.  
  
-   El tipo de datos SQL, precisión y escala del parámetro propio.  
  
-   La dirección de un búfer de longitud/indicador. Proporciona la longitud de bytes de datos binarios o de caracteres, especifica que los datos son NULL o especifica que los datos se enviará con **SQLPutData**. Para obtener más información, consulte [con valores de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Por ejemplo, el siguiente código enlaza *vendedor* y *CustID* a parámetros para las columnas de vendedor y CustID. Dado que *vendedor* contiene datos de caracteres, que es de longitud variable, el código especifica la longitud en bytes de *vendedor* (11) y lo enlaza *SalesPersonLenOrInd* a contiene la longitud de bytes de los datos de *vendedor*. Esta información no es necesaria para *CustID* porque contiene datos de enteros, que es de longitud fija.  
  
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
  
 Cuando **SQLBindParameter** es llama, el controlador almacena esta información en la estructura de la instrucción. Cuando se ejecuta la instrucción, usa la información para recuperar los datos del parámetro y enviarlo al origen de datos.  
  
> [!NOTE]  
>  En ODBC 1.0, los parámetros se enlazan con **SQLSetParam**. El Administrador de controladores asigna las llamadas entre **SQLSetParam** y **SQLBindParameter**, en función de las versiones de ODBC utilizada por la aplicación y el controlador.
