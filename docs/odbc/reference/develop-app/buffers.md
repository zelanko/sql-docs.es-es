---
title: Búferes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad13379552e3a5a576b0aa5cc8720ca6ca1688a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118743"
---
# <a name="buffers"></a>Búferes
Un búfer es cualquier parte de la memoria de la aplicación usa para pasar datos entre la aplicación y el controlador. Por ejemplo, búferes de la aplicación se pueden asociar, o *enlazado,* columnas con el conjunto de resultados **SQLBindCol**. Cada fila se capturan, los datos se devuelven para cada columna en estos búferes. *Los búferes de entrada* se utilizan para pasar datos de la aplicación para el controlador; *los búferes de salida* se utilizan para devolver datos desde el controlador a la aplicación.  
  
> [!NOTE]  
>  Si una función ODBC devuelve SQL_ERROR, el contenido de cualquier parámetro de salida a esa función es indefinido.  
  
 Esta explicación se refiere principalmente con búferes de tipo indeterminado. Las direcciones de estos búferes aparecen como argumentos de tipo SQLPOINTER, como el *TargetValuePtr* argumento en **SQLBindCol**. Sin embargo, algunos de los elementos que se tratan aquí, por ejemplo, los argumentos usados con búferes, también se aplican a los argumentos que se usan para pasar cadenas al controlador, como el *TableName* argumento en **SQLTables**.  
  
 Estos búferes normalmente vienen en pares. *Los búferes de datos* son usa para pasar los datos en Sí, mientras *búferes de longitud/indicador* se utilizan para pasar la longitud de los datos en el búfer de datos o un valor especial como SQL_NULL_DATA, lo que indica que los datos son NULL. La longitud de los datos en un búfer de datos es diferente de la longitud del búfer de datos propia. La siguiente ilustración muestra la relación entre el búfer de datos y búfer indicador de longitud.  
  
 ![Búfer de datos y la longitud&#47;búfer indicador](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Un búfer de longitud/indicador es necesario cuando el búfer de datos contiene datos de longitud variable, como caracteres o datos binarios. Si el búfer de datos contiene datos de longitud fija, como una estructura de entero o una fecha, un búfer de longitud/indicador solo es necesario para pasar valores de indicador porque ya se conoce la longitud de los datos. Si una aplicación utiliza un búfer de longitud/indicador con datos de longitud fija, el controlador omite cualquier longitudes pasadas en ella.  
  
 La longitud del búfer de datos y los datos que contiene se mide en bytes, en lugar de caracteres. Esta distinción es importante para programas que utilizan las cadenas ANSI porque las longitudes de bytes y caracteres son iguales.  
  
 Cuando el búfer de datos representa un campo descriptor definidos por el controlador, el campo de diagnóstico o el atributo, la aplicación debe indicar al administrador de controladores la naturaleza del argumento de función que indica el valor del campo o atributo. La aplicación hace esto estableciendo el argumento de longitud de cualquier llamada de función que establece el campo o atributo en uno de los siguientes valores. (El mismo es cierto para las funciones que recuperen los valores del campo o atributo, con la excepción de que el argumento apunta a los valores de la función de configuración en el propio argumento).  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a una cadena de caracteres, el *longitud* argumento es la longitud de la cadena o SQL_NTS.  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a un búfer binario, la aplicación, el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en el *longitud* argumento. Esto coloca un valor negativo en el *longitud* argumento.  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, la *longitud* argumento debe tener el valor SQL_IS_POINTER.  
  
-   Si el argumento de función que indica el valor del campo o atributo contiene un valor de longitud fija, el *longitud* argumento es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_ISI_USMALLINT, según corresponda.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Búferes diferidos](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Utilizar los búferes de datos](../../../odbc/reference/develop-app/using-data-buffers.md)
