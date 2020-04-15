---
title: Obtención de una fila de datos ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a702f561b756d5305020df9f015d3ea4b444caa6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305676"
---
# <a name="fetching-a-row-of-data"></a>Capturar una fila de datos
Para capturar una fila de datos, una aplicación llama a **SQLFetch**. **SQLFetch** se puede llamar con cualquier tipo de cursor, pero solo mueve el cursor del conjunto de filas en una dirección de solo avance. **SQLFetch** avanza el cursor a la fila siguiente y devuelve los datos de las columnas enlazadas con llamadas a **SQLBindCol**. Cuando el cursor llega al final del conjunto de resultados, **SQLFetch** devuelve SQL_NO_DATA. Para obtener ejemplos de llamada a **SQLFetch**, vea Uso de [SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Exactamente cómo se implementa **SQLFetch** es específico del controlador, pero el patrón general es que el controlador recupere los datos de las columnas enlazadas del origen de datos, los convierta según los tipos de las variables enlazadas y coloque los datos convertidos en esas variables. Si el controlador no puede convertir ningún dato, **SQLFetch** devuelve un error. La aplicación puede continuar capturando filas, pero se pierden los datos de la fila actual. Lo que sucede con los datos de las columnas sin enlazar depende del controlador, pero la mayoría de los controladores los recuperan y descartan o nunca los recuperan en absoluto.  
  
 El controlador también establece los valores de los búferes de longitud/indicador que se han enlazado. Si el valor de datos de una columna es NULL, el controlador establece el búfer de longitud/indicador correspondiente en SQL_NULL_DATA. Si el valor de datos no es NULL, el controlador establece el búfer de longitud/indicador en la longitud de bytes de los datos después de la conversión. Si no se puede determinar esta longitud, como a veces sucede con los datos largos que se recuperan mediante más de una llamada de función, el controlador establece el búfer de longitud/indicador en SQL_NO_TOTAL. Para los tipos de datos de longitud fija, como enteros y estructuras de fecha, la longitud de byte es el tamaño del tipo de datos.  
  
 Para los datos de longitud variable, como datos binarios y de caracteres, el controlador comprueba la longitud de bytes de los datos convertidos con la longitud de bytes del búfer enlazado a la columna; la longitud del búfer se especifica en el argumento *BufferLength* de **SQLBindCol**. Si la longitud de bytes de los datos convertidos es mayor que la longitud de bytes del búfer, el controlador trunca los datos para que quepan en el búfer, devuelve la longitud no truncada en el búfer de longitud/indicador, devuelve SQL_SUCCESS_WITH_INFO y coloca SQLSTATE 01004 (datos truncados) en los diagnósticos. La única excepción a esto es si un marcador de longitud variable se trunca cuando **SQLFetch**lo devuelve , que devuelve SQLSTATE 22001 (datos de cadena, truncados a la derecha).  
  
 Los datos de longitud fija nunca se truncan, porque el controlador supone que el tamaño del búfer enlazado es el tamaño del tipo de datos. El truncamiento de datos tiende a ser poco frecuente, porque la aplicación normalmente enlaza un búfer lo suficientemente grande como para contener todo el valor de datos; determina el tamaño necesario a partir de los metadatos. Sin embargo, la aplicación podría enlazar explícitamente un búfer que sabe que es demasiado pequeño. Por ejemplo, podría recuperar y mostrar los primeros 20 caracteres de una descripción de pieza o los primeros 100 caracteres de una columna de texto largo.  
  
 El controlador debe terminar los datos de caracteres antes de que se devuelvan a la aplicación, incluso si se ha truncado. El carácter de terminación nula no se incluye en la longitud de bytes devuelta, pero requiere espacio en el búfer enlazado. Por ejemplo, supongamos que una aplicación utiliza cadenas compuestas de datos de caracteres en el juego de caracteres ASCII, un controlador tiene 50 caracteres de datos para devolver y el búfer de la aplicación tiene 25 bytes de longitud. En el búfer de la aplicación, el controlador devuelve los primeros 24 caracteres seguidos de un carácter de terminación nula. En el búfer de longitud/indicador, devuelve una longitud de byte de 50.  
  
 La aplicación puede restringir el número de filas del conjunto de resultados estableciendo el atributo de instrucción SQL_ATTR_MAX_ROWS antes de ejecutar la instrucción que crea el conjunto de resultados. Por ejemplo, el modo de vista previa en una aplicación utilizada para dar formato a los informes solo necesita suficientes datos para mostrar la primera página del informe. Al restringir el tamaño del conjunto de resultados, dicha característica se ejecutaría más rápido. Este atributo de instrucción está pensado para reducir el tráfico de red y es posible que todos los controladores no lo admitan.
