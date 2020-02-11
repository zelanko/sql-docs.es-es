---
title: Capturando una fila de datos | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069861"
---
# <a name="fetching-a-row-of-data"></a>Capturar una fila de datos
Para capturar una fila de datos, una aplicación llama a **SQLFetch**. Se puede llamar a **SQLFetch** con cualquier tipo de cursor, pero solo se mueve el cursor del conjunto de filas en una dirección de solo avance. **SQLFetch** hace avanzar el cursor hasta la siguiente fila y devuelve los datos de las columnas que estaban enlazadas con llamadas a **SQLBindCol**. Cuando el cursor alcanza el final del conjunto de resultados, **SQLFetch** devuelve SQL_NO_DATA. Para obtener ejemplos de cómo llamar a **SQLFetch**, vea [usar SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Exactamente cómo se implementa **SQLFetch** es específico del controlador, pero el patrón general es que el controlador recupere los datos de las columnas enlazadas del origen de datos, los convierte en función de los tipos de las variables enlazadas y coloca los datos convertidos en esas variables. Si el controlador no puede convertir datos, **SQLFetch** devuelve un error. La aplicación puede seguir recuperando filas, pero se pierden los datos de la fila actual. Lo que sucede con los datos de las columnas sin enlazar depende del controlador, pero la mayoría de los controladores lo recuperan y descartan, o nunca lo recuperan.  
  
 El controlador también establece los valores de cualquier búfer de longitud/indicador que se haya enlazado. Si el valor de los datos de una columna es NULL, el controlador establece el búfer de longitud/indicador correspondiente en SQL_NULL_DATA. Si el valor de los datos no es NULL, el controlador establece el búfer de longitud/indicador en la longitud de bytes de los datos después de la conversión. Si no se puede determinar esta longitud, como es en ocasiones el caso con datos largos recuperados por más de una llamada de función, el controlador establece el búfer de longitud/indicador en SQL_NO_TOTAL. En el caso de los tipos de datos de longitud fija, como enteros y estructuras de fecha, la longitud de bytes es el tamaño del tipo de datos.  
  
 En el caso de los datos de longitud variable, como los datos de caracteres y binarios, el controlador comprueba la longitud de bytes de los datos convertidos con respecto a la longitud de bytes del búfer enlazado a la columna; la longitud del búfer se especifica en el argumento *BufferLength* de **SQLBindCol**. Si la longitud de bytes de los datos convertidos es mayor que la longitud de bytes del búfer, el controlador trunca los datos para ajustarse al búfer, devuelve la longitud sin truncar en el búfer de longitud/indicador, devuelve SQL_SUCCESS_WITH_INFO y coloca SQLSTATE 01004 (datos truncados) en el diagnóstico. La única excepción a esto es si un marcador de longitud variable se trunca cuando lo devuelve **SQLFetch**, que devuelve SQLSTATE 22001 (datos de cadena, truncados a la derecha).  
  
 Los datos de longitud fija nunca se truncan, porque el controlador supone que el tamaño del búfer enlazado es el tamaño del tipo de datos. El truncamiento de datos tiende a ser poco frecuente, porque la aplicación suele enlazar un búfer lo suficientemente grande como para contener todo el valor de datos; determina el tamaño necesario de los metadatos. Sin embargo, es posible que la aplicación enlace explícitamente un búfer que sabe que es demasiado pequeño. Por ejemplo, podría recuperar y mostrar los primeros 20 caracteres de una descripción de parte o los primeros 100 caracteres de una columna de texto largo.  
  
 Los datos de caracteres deben terminar en NULL el controlador antes de que se devuelvan a la aplicación, incluso si se han truncado. El carácter de terminación NULL no se incluye en la longitud de bytes devuelta, pero sí requiere espacio en el búfer enlazado. Por ejemplo, supongamos que una aplicación utiliza cadenas que se componen de datos de caracteres en el juego de caracteres ASCII, un controlador tiene 50 caracteres de datos para devolver y el búfer de la aplicación tiene una longitud de 25 bytes. En el búfer de la aplicación, el controlador devuelve los 24 primeros caracteres seguidos de un carácter de terminación null. En el búfer de longitud/indicador, devuelve una longitud de bytes de 50.  
  
 La aplicación puede restringir el número de filas del conjunto de resultados estableciendo el atributo de instrucción SQL_ATTR_MAX_ROWS antes de ejecutar la instrucción que crea el conjunto de resultados. Por ejemplo, el modo de vista previa en una aplicación que se usa para dar formato a los informes solo necesita datos suficientes para mostrar la primera página del informe. Al restringir el tamaño del conjunto de resultados, una característica de este tipo se ejecutaría más rápido. Este atributo de instrucción está pensado para reducir el tráfico de red y es posible que no sea compatible con todos los controladores.
