---
title: La longitud del búfer de datos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57f4fd34cfe3896bb29ed31f02906ce675e4b854
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811393"
---
# <a name="data-buffer-length"></a>Longitud del búfer de datos
La aplicación pasa la longitud de bytes del búfer de datos para el controlador en un argumento, denominado *BufferLength* o un nombre similar. Por ejemplo, en la siguiente llamada a **SQLBindCol**, la aplicación especifica la longitud de la *ValuePtr* búfer (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Un controlador siempre devolverá el número de bytes, no el número de caracteres, en el argumento de longitud de búfer de cualquier función que tiene un argumento de cadena de salida.  
  
 Las longitudes de búfer de datos solo son necesarias para los búferes de salida; el controlador utiliza para evitar escribir más allá del final del búfer. Sin embargo, el controlador comprueba la longitud del búfer de datos solo cuando el búfer contiene datos de longitud variable, como caracteres o datos binarios. Si el búfer contiene datos de longitud fija, como una estructura de entero o una fecha, el controlador pasa por alto la longitud del búfer de datos y se supone que el búfer es suficientemente grande como para contener los datos; es decir, nunca trunca los datos de longitud fija. Por lo tanto, es importante para la aplicación asignar un búfer suficientemente grande como para los datos de longitud fija.  
  
 Cuando las cadenas de salida de un truncamiento de datos no se produce (como el nombre del cursor devuelto para **SQLGetCursorName**), la longitud devuelta en el argumento de longitud de búfer es la longitud máxima de caracteres posible.  
  
 Las longitudes de búfer de datos no son necesarias para los búferes de entrada dado que el controlador no escriben en estos búferes.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Con los valores de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [Longitud de los datos, la longitud de búfer y truncamiento](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [Datos de caracteres y cadenas de c](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
