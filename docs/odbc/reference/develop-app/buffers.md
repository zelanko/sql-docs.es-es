---
title: Zonas de influencia ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c49e83e12463665f86f8cc15dc595e6ba2c506f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306290"
---
# <a name="buffers"></a>Búferes
Un búfer es cualquier parte de la memoria de la aplicación que se utiliza para pasar datos entre la aplicación y el controlador. Por ejemplo, los búferes de aplicación se pueden asociar o *enlazar a* columnas de conjunto de resultados con **SQLBindCol**. A medida que se recupera cada fila, se devuelven los datos para cada columna de estos búferes. *Los búferes* de entrada se utilizan para pasar datos de la aplicación al controlador; *los búferes* de salida se utilizan para devolver datos del controlador a la aplicación.  
  
> [!NOTE]  
>  Si una función ODBC devuelve SQL_ERROR, el contenido de los argumentos de salida de esa función es indefinido.  
  
 Esta discusión se refiere principalmente a los búferes de tipo indeterminado. Las direcciones de estos búferes aparecen como argumentos de tipo SQLPOINTER, como el *TargetValuePtr* argumento en **SQLBindCol**. Sin embargo, algunos de los elementos que se describen aquí, como los argumentos utilizados con los búferes, también se aplican a los argumentos utilizados para pasar cadenas al controlador, como el argumento *TableName* en **SQLTables**.  
  
 Estos buffers generalmente vienen en pares. *Los búferes* de datos se utilizan para pasar los propios datos, mientras que los búferes de *longitud/indicador* se utilizan para pasar la longitud de los datos en el búfer de datos o un valor especial como SQL_NULL_DATA, lo que indica que los datos son NULL. La longitud de los datos en un búfer de datos es diferente de la longitud del propio búfer de datos. En la ilustración siguiente se muestra la relación entre el búfer de datos y el búfer de longitud/indicador.  
  
 ![Búfer de datos y longitud&#47;búfer del indicador](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Se requiere un búfer de longitud/indicador siempre que el búfer de datos contenga datos de longitud variable, como datos binarios o de caracteres. Si el búfer de datos contiene datos de longitud fija, como un entero o una estructura de fecha, solo se necesita un búfer de longitud/indicador para pasar valores de indicador porque la longitud de los datos ya se conoce. Si una aplicación utiliza un búfer de longitud/indicador con datos de longitud fija, el controlador omite las longitudes que se pasan en él.  
  
 La longitud del búfer de datos y los datos que contiene se mide en bytes, a diferencia de los caracteres. Esta distinción no es importante para los programas que utilizan cadenas ANSI porque las longitudes en bytes y caracteres son las mismas.  
  
 Cuando el búfer de datos representa un campo descriptor definido por el controlador, un campo de diagnóstico o un atributo, la aplicación debe indicar al Administrador de controladores la naturaleza del argumento de función que indica el valor del campo o atributo. Para ello, la aplicación establece el argumento length en cualquier llamada de función que establezca el campo o atributo en uno de los siguientes valores. (Lo mismo es cierto para las funciones que recuperan los valores del campo o atributo, con la excepción de que el argumento apunta a los valores que para la función de configuración están en el propio argumento.)  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a una cadena de caracteres, el argumento *length* es la longitud de la cadena o SQL_NTS.  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a un búfer binario, la aplicación coloca el resultado de la macro SQL_LEN_BINARY_ATTR(*length*) en el argumento *length.* Esto coloca un valor negativo en el argumento *length.*  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, el argumento *length* debe tener el valor SQL_IS_POINTER.  
  
-   Si el argumento de función que indica el valor del campo o atributo contiene un valor de longitud fija, el argumento *length* es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_ISI_USMALLINT, según corresponda.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Búferes diferidos](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Utilizar los búferes de datos](../../../odbc/reference/develop-app/using-data-buffers.md)
