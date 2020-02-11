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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118743"
---
# <a name="buffers"></a>Búferes
Un búfer es cualquier parte de la memoria de la aplicación que se usa para pasar datos entre la aplicación y el controlador. Por ejemplo, los búferes de aplicación pueden asociarse a columnas del conjunto de resultados, o *enlazarse a ellas,* con **SQLBindCol**. A medida que se capturan todas las filas, se devuelven los datos de cada columna de estos búferes. Los *búferes de entrada* se utilizan para pasar datos de la aplicación al controlador; los *búferes de salida* se usan para devolver datos del controlador a la aplicación.  
  
> [!NOTE]  
>  Si una función ODBC devuelve SQL_ERROR, el contenido de los argumentos de salida de la función no está definido.  
  
 Este debate se refiere principalmente a los búferes de tipo indeterminado. Las direcciones de estos búferes aparecen como argumentos de tipo SQLPOINTER, como el argumento *TargetValuePtr* en **SQLBindCol**. Sin embargo, algunos de los elementos que se describen aquí, como los argumentos usados con los búferes, también se aplican a los argumentos utilizados para pasar cadenas al controlador, como el argumento *TableName* en **SQLTables**.  
  
 Estos búferes suelen estar en parejas. Los *búferes de datos* se utilizan para pasar los datos, mientras que los *búferes de longitud/indicador* se utilizan para pasar la longitud de los datos en el búfer de datos o un valor especial, como SQL_NULL_DATA, que indica que los datos son NULL. La longitud de los datos en un búfer de datos es diferente de la longitud del búfer de datos en sí. En la ilustración siguiente se muestra la relación entre el búfer de datos y el búfer de longitud/indicador.  
  
 ![Búfer de datos y búfer indicador de longitud&#47;](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Se requiere un búfer de longitud/indicador cuando el búfer de datos contiene datos de longitud variable, como datos de caracteres o binarios. Si el búfer de datos contiene datos de longitud fija, como un entero o una estructura de fecha, solo se necesita un búfer de longitud/indicador para pasar valores de indicador porque ya se conoce la longitud de los datos. Si una aplicación usa un búfer de longitud/indicador con datos de longitud fija, el controlador omite cualquier longitud pasada.  
  
 La longitud del búfer de datos y de los datos que contiene se mide en bytes, en lugar de en caracteres. Esta distinción no es importante para los programas que usan cadenas ANSI porque las longitudes en bytes y caracteres son iguales.  
  
 Cuando el búfer de datos representa un campo de descriptor definido por el controlador, un campo de diagnóstico o un atributo, la aplicación debe indicar al administrador de controladores la naturaleza del argumento de función que indica el valor del campo o atributo. Para ello, la aplicación establece el argumento de longitud en cualquier llamada de función que establezca el campo o el atributo en uno de los valores siguientes. (Lo mismo sucede con las funciones que recuperan los valores del campo o atributo, con la excepción de que el argumento apunta a los valores que para la función de configuración están en el propio argumento).  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a una cadena de caracteres, el argumento de *longitud* es la longitud de la cadena o SQL_NTS.  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a un búfer binario, la aplicación coloca el resultado de la macro de SQL_LEN_BINARY_ATTR (*longitud*) en el argumento de *longitud* . Esto coloca un valor negativo en el argumento de *longitud* .  
  
-   Si el argumento de función que indica el valor del campo o atributo es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, el argumento de *longitud* debe tener el valor SQL_IS_POINTER.  
  
-   Si el argumento de función que indica el valor del campo o atributo contiene un valor de longitud fija, el argumento de *longitud* es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_ISI_USMALLINT, según corresponda.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Búferes diferidos](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Utilizar los búferes de datos](../../../odbc/reference/develop-app/using-data-buffers.md)
