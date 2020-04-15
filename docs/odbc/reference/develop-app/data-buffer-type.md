---
title: Tipo de búfer de datos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b98ed2ab0865b98884f6dfa1ff20142540ff314
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305251"
---
# <a name="data-buffer-type"></a>Tipo de búfer de datos
La aplicación especifica el tipo de datos C de un búfer. Con una sola variable, esto ocurre cuando la aplicación asigna la variable. Con la memoria genérica, es decir, la memoria señalada por un puntero de tipo void, esto ocurre cuando la aplicación convierte la memoria en un tipo determinado. El controlador descubre este tipo de dos maneras:  
  
-   **Argumento de tipo de búfer de datos.** Los búferes utilizados para transferir valores de parámetro y datos de conjunto de resultados, como el búfer enlazado con *TargetValuePtr* en **SQLBindCol**, suelen tener un argumento de tipo asociado, como el argumento *TargetType* en **SQLBindCol**. En este argumento, la aplicación pasa el identificador de tipo C que corresponde al tipo del búfer. Por ejemplo, en la siguiente llamada a **SQLBindCol**, el valor SQL_C_TYPE_DATE indica al controlador que el búfer *Date* es un SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Para obtener más información acerca de los identificadores de tipo, vea la sección Tipos de [datos en ODBC,](../../../odbc/reference/develop-app/data-types-in-odbc.md) más adelante en esta sección.  
  
-   **Tipo predefinido.** Los búferes utilizados para enviar y recuperar opciones o atributos, como el búfer al que apunta el argumento *InfoValuePtr* en **SQLGetInfo**, tienen un tipo fijo que depende de la opción especificada. El controlador supone que el búfer de datos es de este tipo; es responsabilidad de la aplicación asignar un búfer de este tipo. Por ejemplo, en la siguiente llamada a **SQLGetInfo**, el controlador asume que el búfer es un entero de 32 bits porque esto es lo que requiere la opción SQL_STRING_FUNCTIONS:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 El controlador utiliza el tipo de datos C para interpretar los datos en el búfer.
