---
title: Búferes | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d63aa103ac71aa89d245f6b8e4770b2c4943f2a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="buffers"></a>Búferes
Un búfer es cualquier parte de la memoria de la aplicación usa para pasar datos entre la aplicación y el controlador. Por ejemplo, búferes de la aplicación pueden estar asociados, o *enlazado y* columnas con el conjunto de resultados **SQLBindCol**. Tal y como se recupera cada fila, los datos se devuelven para cada columna en estos búferes. *Búferes de entrada* se utilizan para pasar datos de la aplicación para el controlador; *búferes de salida* se utilizan para devolver datos desde el controlador a la aplicación.  
  
> [!NOTE]  
>  Si una función ODBC devuelve SQL_ERROR, el contenido de cualquier parámetro de salida a esa función es indefinido.  
  
 Esta descripción está relacionada principalmente con búferes de tipo indeterminado. Las direcciones de estos búferes aparecen como argumentos de tipo SQLPOINTER, como el *TargetValuePtr* argumento en **SQLBindCol**. Sin embargo, algunos de los elementos que se tratan aquí, por ejemplo, los argumentos usados con búferes, también se aplican a los argumentos que se usan para pasar cadenas al controlador, como el *TableName* argumento en **SQLTables**.  
  
 Estos búferes normalmente vienen en parejas. *Los búferes de datos* son mientras que se utiliza para pasar los datos en Sí, *búferes de longitud/indicador* se utilizan para pasar la longitud de los datos en el búfer de datos o un valor especial como SQL_NULL_DATA, lo que indica que los datos son NULL. La longitud de los datos en un búfer de datos es diferente de la longitud del búfer de datos propia. En la siguiente ilustración muestra la relación entre el búfer de datos y el búfer de longitud/indicador.  
  
 ![Búfer de datos y longitud&#47;búfer indicador](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Se requiere un búfer de longitud/indicador cada vez que el búfer de datos contiene datos de longitud variable, como datos de caracteres o binarios. Si el búfer de datos contiene datos de longitud fija, como una estructura de entero o una fecha, se necesita un búfer de longitud/indicador solo para pasar valores de indicador porque ya se conoce la longitud de los datos. Si una aplicación utiliza un búfer de longitud/indicador con datos de longitud fija, el controlador omite cualquier longitudes pasados en ella.  
  
 La longitud del búfer de datos y los datos que contiene se mide en bytes, en lugar de caracteres. Esta distinción es importante para programas que utilizan cadenas ANSI porque la longitud en bytes y caracteres es los mismos.  
  
 Cuando el búfer de datos representa un campo descriptor definidos por el controlador, diagnóstico campo o atributo, la aplicación debe indicar al administrador de controladores la naturaleza del argumento de función que indica el valor para el campo o atributo. La aplicación lleva esto estableciendo el argumento length en ninguna llamada de función que establece el campo o atributo a uno de los siguientes valores. (Lo mismo sirve para funciones que recuperen los valores del campo o atributo, con la excepción de que el argumento apunta a los valores de la función de configuración en el propio argumento.)  
  
-   Si el argumento de función que indica el valor para el campo o atributo es un puntero a una cadena de caracteres, el *longitud* argumento es la longitud de la cadena o SQL_NTS.  
  
-   Si el argumento de función que indica el valor para el campo o atributo es un puntero a un búfer binario, la aplicación coloca el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en el *longitud* argumento pasado. Esto coloca un valor negativo en el *longitud* argumento.  
  
-   Si el argumento de función que indica el valor para el campo o atributo es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, la *longitud* argumento debe tener el valor SQL_IS_POINTER.  
  
-   Si el argumento de función que indica el valor para el campo o atributo contiene un valor de longitud fija, el *longitud* argumento es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_ISI_USMALLINT, según corresponda.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Búferes diferidos](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Utilizar los búferes de datos](../../../odbc/reference/develop-app/using-data-buffers.md)
