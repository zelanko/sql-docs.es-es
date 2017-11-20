---
title: "Tipo de búfer de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c2ed3fb1d6a68737a894663e1b5c841d6cb1041
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="data-buffer-type"></a>Tipo de búfer de datos
El tipo de datos C de un búfer especificado por la aplicación. Con una variable simple, esto se produce cuando la aplicación asigna la variable. Con genéricos de memoria, es decir, memoria indicada por un puntero de tipo void, esto se produce cuando la aplicación convierte la memoria a un tipo determinado. El controlador detecta este tipo de dos maneras:  
  
-   **Argumento de tipo de búfer de datos.** Búferes que usa para transferir valores de parámetro y de datos del conjunto de resultados, como el búfer enlazado con *TargetValuePtr* en **SQLBindCol**, normalmente tiene un argumento de tipo asociado, como el  *TargetType* argumento en **SQLBindCol**. En este argumento, la aplicación pasa el identificador de tipo de C que corresponde al tipo de búfer. Por ejemplo, en la siguiente llamada a **SQLBindCol**, el valor SQL_C_TYPE_DATE indica al controlador que la *fecha* búfer es un SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Para obtener más información acerca de los identificadores de tipo, consulte el [tipos de datos de ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) sección, más adelante en esta sección.  
  
-   **Tipo predefinido.** Búferes que usa para enviar y recuperar opciones o atributos, como el búfer señalado por el *InfoValuePtr* argumento en **SQLGetInfo**, tienen un tipo fijo que depende de la opción especificada. El controlador se da por supuesto que el búfer de datos es de este tipo; es responsabilidad de la aplicación para asignar un búfer de este tipo. Por ejemplo, en la siguiente llamada a **SQLGetInfo**, el controlador se da por supuesto que el búfer es un entero de 32 bits porque esto es lo que requiere la opción SQL_STRING_FUNCTIONS:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 El controlador utiliza el tipo de datos de C para interpretar los datos en el búfer.

