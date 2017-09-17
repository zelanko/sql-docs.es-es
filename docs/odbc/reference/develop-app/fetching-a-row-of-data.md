---
title: Capturar una fila de datos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 142c9a2c95900e5b3776f96d86a145defc447512
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="fetching-a-row-of-data"></a>Capturar una fila de datos
Para capturar una fila de datos, una aplicación llama **SQLFetch**. **SQLFetch** se puede llamar con cualquier tipo de cursor, pero solo mueve el cursor de conjunto de filas en una dirección de solo avance. **SQLFetch** avanza el cursor a la siguiente fila y devuelve los datos de todas las columnas que se enlazaron con llamadas a **SQLBindCol**. Cuando el cursor llega al final del resultado se establece, **SQLFetch** devuelve SQL_NO_DATA. Para obtener ejemplos de llamar al método **SQLFetch**, consulte [utilizando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Exactamente cómo **SQLFetch** se implementa es específico del controlador, pero la ficha general patrón es el controlador recuperar los datos para cualquier enlaza las columnas del origen de datos, convertirla según los tipos de las variables enlazadas y coloque el datos convertidos en esas variables. Si el controlador no puede convertir cualquier dato, **SQLFetch** devuelve un error. La aplicación puede continuar la captura de filas, pero se pierden los datos de la fila actual. ¿Qué ocurre con los datos de las columnas sin enlazar depende del controlador, pero la mayoría de los controladores recuperar y descartar los cambios o nunca recuperarlo.  
  
 El controlador también establece los valores de cualquier búfer de longitud/indicador que se han enlazado. Si el valor de datos para una columna es NULL, el controlador establece el búfer de longitud/indicador correspondiente en SQL_NULL_DATA. Si el valor de datos no es NULL, el controlador establece el búfer de longitud/indicador en la longitud de bytes de los datos después de la conversión. Si no se puede determinar la longitud de esta, como sucede en ocasiones con datos de tipo long que se recuperan más de una llamada de función, el controlador establece el búfer de longitud/indicador en SQL_NO_TOTAL. Para los tipos de datos de longitud fija, como enteros y estructuras de fecha, la longitud de bytes es el tamaño del tipo de datos.  
  
 Para los datos de longitud variable, como datos de caracteres y binarios, el controlador comprueba la longitud de bytes de los datos convertidos en la longitud de bytes del búfer enlazada a la columna; longitud del búfer se especifica en el *BufferLength* argumento en **SQLBindCol**. Si la longitud de bytes de los datos convertidos es mayor que la longitud de bytes del búfer, el controlador trunca los datos para que quepa en el búfer, se devuelve la longitud del búfer de longitud/indicador untruncated devuelve SQL_SUCCESS_WITH_INFO y lo coloca SQLSTATE 01004 (datos trunca) en el diagnóstico. La única excepción a esto es si un marcador de longitud variable se trunca cuando devuelve **SQLFetch**, que devuelve SQLSTATE 22001 (datos de cadena, truncados por la derecha).  
  
 Nunca se truncan los datos de longitud fija, porque el controlador da por hecho que el tamaño del búfer enlazado es el tamaño del tipo de datos. Truncamiento de datos tiende a ser poco frecuente, porque la aplicación enlaza normalmente un búfer lo suficientemente grande como para contener el valor de datos completa; Determina el tamaño de los metadatos necesario. Sin embargo, la aplicación podría enlazar explícitamente un búfer que sepa que puede para ser demasiado pequeño. Por ejemplo, puede recuperar y mostrar los 20 primeros caracteres de la descripción de una parte o los 100 primeros caracteres de una columna de texto largo.  
  
 Datos de caracteres deben ser el controlador terminada en null antes de que se devuelva a la aplicación, incluso si se ha truncado. El carácter de terminación null no se incluye en la longitud de bytes devuelto pero requieren espacio en el búfer de enlazado. Por ejemplo, suponga que una aplicación utiliza cadenas formadas por datos de caracteres del juego de caracteres ASCII, un controlador tiene 50 caracteres de datos que se va a devolver y búfer de la aplicación tiene una longitud de 25 bytes. En el búfer de la aplicación, el controlador devuelve los primeros 24 caracteres seguidos por un carácter de terminación null. En el búfer de longitud/indicador, devuelve una longitud de bytes de 50.  
  
 La aplicación puede restringir el número de filas del conjunto estableciendo el atributo de instrucción de SQL_ATTR_MAX_ROWS antes de ejecutar la instrucción que crea el resultado de conjunto de resultados. Por ejemplo, el modo de vista previa en una aplicación que se utilizan para dar formato a informes solamente necesita suficientes datos para mostrar la primera página del informe. Al restringir el tamaño del conjunto de resultados, esta característica llevarían a cabo con mayor rapidez. Este atributo de instrucción está pensado para reducir el tráfico de red y podría no ser compatibles con todos los controladores.
