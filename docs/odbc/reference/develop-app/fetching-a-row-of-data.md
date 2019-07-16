---
title: Capturar una fila de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 010d05990396c10836c0a2130e5d9f4392ae56ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069861"
---
# <a name="fetching-a-row-of-data"></a>Capturar una fila de datos
Para capturar una fila de datos, una aplicación llama a **SQLFetch**. **SQLFetch** se puede llamar con cualquier tipo de cursor, pero solo mueve el cursor de conjunto de filas en una dirección de solo avance. **SQLFetch** hace avanzar el cursor a la siguiente fila y devuelve los datos para las columnas que se enlazaron con llamadas a **SQLBindCol**. Cuando el cursor llega al final del resultado se establece, **SQLFetch** devuelve SQL_NO_DATA. Para obtener ejemplos de llamada **SQLFetch**, consulte [utilizando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Exactamente cómo **SQLFetch** se implementa es específico del controlador, pero en general es el patrón para que el controlador recuperar los datos para cualquier enlaza las columnas del origen de datos, convertirla según los tipos de las variables enlazadas y coloque el datos convertidos en esas variables. Si el controlador no puede convertir cualquier dato, **SQLFetch** devuelve un error. La aplicación puede continuar la captura de filas, pero se pierden los datos de la fila actual. ¿Qué ocurre con los datos de las columnas sin enlazar depende del controlador, pero la mayoría de los controladores recuperar y descartarlo o nunca recuperarlo.  
  
 El controlador también establece los valores de los búferes de longitud/indicador que se han enlazado. Si el valor de datos para una columna es NULL, el controlador establece el búfer de longitud/indicador correspondiente en SQL_NULL_DATA. Si el valor de datos no es NULL, el controlador establece el búfer de longitud/indicador en la longitud de bytes de los datos después de la conversión. Si esta longitud no se puede determinar, en ocasiones, es el caso de los datos de tipo long que se recuperan más de una llamada de función, el controlador establece el búfer de longitud/indicador en SQL_NO_TOTAL. Para los tipos de datos de longitud fija, como enteros y estructuras de fecha, la longitud en bytes es el tamaño del tipo de datos.  
  
 Para los datos de longitud variable, como datos de caracteres y binarios, el controlador comprueba la longitud de bytes de los datos convertidos en la longitud de bytes del búfer enlazada a la columna; longitud del búfer se especifica en el *BufferLength* argumento en **SQLBindCol**. Si la longitud de bytes de los datos convertidos es mayor que la longitud de bytes del búfer, el controlador trunca los datos para que quepa en el búfer, se devuelve la longitud del búfer de longitud/indicador sin truncar devuelve SQL_SUCCESS_WITH_INFO y lo coloca SQLSTATE 01004 (datos truncado) en los diagnósticos. La única excepción a esto es si un marcador de longitud variable se trunca cuando devuelve **SQLFetch**, que devuelve SQLSTATE 22001 (datos de cadena, truncados derecha).  
  
 Nunca se truncan los datos de longitud fija, porque el controlador se da por supuesto que el tamaño del búfer dependiente es el tamaño del tipo de datos. Truncamiento de datos tiende a ser es poco habitual, ya que la aplicación normalmente enlaza un búfer suficientemente grande para contener el valor de datos completa; Determina el tamaño de los metadatos necesario. Sin embargo, la aplicación podría enlazar explícitamente un búfer que sepa que puede para ser demasiado pequeño. Por ejemplo, podría recuperar y mostrar los 20 primeros caracteres de una descripción de la parte o los 100 primeros caracteres de una columna de texto largo.  
  
 Datos de caracteres deben ser terminada en null por el controlador antes de devolverlos a la aplicación, incluso si se ha truncado. El carácter de terminación null no se incluye en la longitud de bytes devuelta, pero requieren espacio en el búfer de enlazado. Por ejemplo, suponga que una aplicación utiliza cadenas formadas por los datos de caracteres en el juego de caracteres ASCII, un controlador tiene 50 caracteres de datos que se va a devolver y búfer de la aplicación tiene una longitud de bytes de 25. En el búfer de la aplicación, el controlador devuelve los primeros 24 caracteres seguidos por un carácter de terminación null. En el búfer de longitud/indicador, devuelve una longitud de bytes de 50.  
  
 La aplicación puede restringir el número de filas del conjunto estableciendo el atributo de instrucción SQL_ATTR_MAX_ROWS antes de ejecutar la instrucción que crea el resultado de conjunto de resultados. Por ejemplo, el modo de vista previa en una aplicación utilizada para dar formato a informes necesita sólo suficientes datos para mostrar la primera página del informe. Al restringir el tamaño del conjunto de resultados, una de estas características se ejecutaría con mayor rapidez. Este atributo de instrucción está pensado para reducir el tráfico de red y no puede ser compatibles con todos los controladores.
