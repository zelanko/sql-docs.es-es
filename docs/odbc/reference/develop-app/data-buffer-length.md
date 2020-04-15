---
title: Longitud del búfer de datos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4a4e9a739201d74cfc6c4f7c18e64b91e0fabe4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305266"
---
# <a name="data-buffer-length"></a>Longitud del búfer de datos
La aplicación pasa la longitud de bytes del búfer de datos al controlador en un argumento, denominado *BufferLength* o un nombre similar. Por ejemplo, en la siguiente llamada a **SQLBindCol**, la aplicación especifica la longitud del búfer *ValuePtr* (**sizeof(***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Un controlador siempre devolverá el número de bytes, no el número de caracteres, en el argumento de longitud de búfer de cualquier función que tenga un argumento de cadena de salida.  
  
 Las longitudes de búfer de datos solo son necesarias para los búferes de salida; el controlador los utiliza para evitar escribir más allá del final del búfer. Sin embargo, el controlador comprueba la longitud del búfer de datos solo cuando el búfer contiene datos de longitud variable, como datos binarios o de caracteres. Si el búfer contiene datos de longitud fija, como un entero o una estructura de fecha, el controlador omite la longitud del búfer de datos y supone que el búfer es lo suficientemente grande como para contener los datos; es decir, nunca trunca los datos de longitud fija. Por lo tanto, es importante que la aplicación asigne un búfer lo suficientemente grande para los datos de longitud fija.  
  
 Cuando se produce un truncamiento de cadenas de salida que no son de datos (como el nombre del cursor devuelto para **SQLGetCursorName**), la longitud devuelta en el argumento de longitud de búfer es la longitud máxima de caracteres posible.  
  
 Las longitudes de búfer de datos no son necesarias para los búferes de entrada porque el controlador no escribe en estos búferes.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de valores de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [Longitud de los datos, la longitud de búfer y truncamiento](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [Datos de caracteres y cadenas de c](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
