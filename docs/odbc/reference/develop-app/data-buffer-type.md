---
title: Tipo de búfer de datos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 615625ca396e5f2ae094962457cc9e746730ddcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067413"
---
# <a name="data-buffer-type"></a>Tipo de búfer de datos
La aplicación especifica el tipo de datos C de un búfer. Con una sola variable, esto se produce cuando la aplicación asigna la variable. Con memoria genérica, es decir, la memoria a la que apunta un puntero de tipo void, se produce cuando la aplicación convierte la memoria en un tipo determinado. El controlador detecta este tipo de dos maneras:  
  
-   **Argumento de tipo de búfer de datos.** Los búferes que se usan para transferir valores de parámetros y datos del conjunto de resultados, como el búfer enlazado con *TargetValuePtr* en **SQLBindCol**, normalmente tienen un argumento de tipo asociado, como el argumento *TargetType* en **SQLBindCol**. En este argumento, la aplicación pasa el identificador de tipo de C que corresponde al tipo de búfer. Por ejemplo, en la siguiente llamada a **SQLBindCol**, el valor SQL_C_TYPE_DATE indica al controlador que el búfer de *fecha* es un SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Para obtener más información sobre los identificadores de tipo, vea la sección [tipos de datos en ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) , más adelante en esta sección.  
  
-   **Tipo predefinido.** Los búferes que se usan para enviar y recuperar opciones o atributos, como el búfer señalado por el argumento *InfoValuePtr* en **SQLGetInfo**, tienen un tipo fijo que depende de la opción especificada. El controlador supone que el búfer de datos es de este tipo; es responsabilidad de la aplicación asignar un búfer de este tipo. Por ejemplo, en la siguiente llamada a **SQLGetInfo**, el controlador supone que el búfer es un entero de 32 bits porque es lo que requiere la opción SQL_STRING_FUNCTIONS:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 El controlador utiliza el tipo de datos C para interpretar los datos del búfer.
