---
title: Utilizar matrices de parámetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf6b5127bac7aedf9e67918d38020c73a4afe186
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079598"
---
# <a name="using-arrays-of-parameters"></a>Utilizar matrices de parámetros
Utilizar matrices de parámetros, la aplicación llama a **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_PARAMSET_SIZE para especificar el número de conjuntos de parámetros. Llama a **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_PARAMS_PROCESSED_PTR para especificar la dirección de una variable en el que el controlador puede devolver el número de conjuntos de parámetros procesados, establece el error incluida. Llama a **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_PARAM_STATUS_PTR para que apunte a una matriz en la que se va a devolver información de estado para cada fila de valores de parámetro. El controlador almacena estas direcciones en la estructura que se mantiene para la instrucción.  
  
> [!NOTE]  
>  En ODBC 2. *x*, **SQLParamOptions** llamó para especificar varios valores para un parámetro. En ODBC 3. *x*, la llamada a **SQLParamOptions** ha sido reemplazado por las llamadas a **SQLSetStmtAttr** para establecer los atributos SQL_ATTR_PARAMSET_SIZE y SQL_ATTR_PARAMS_PROCESSED_ARRAY .  
  
 Antes de ejecutar la instrucción, la aplicación establece el valor de cada elemento de cada matriz dependiente. Cuando se ejecuta la instrucción, el controlador utiliza la información almacenada para recuperar los valores de parámetro y enviarlos al origen de datos; Si es posible, el controlador debe enviar estos valores como matrices. Aunque el uso de matrices de parámetros se implementa mejor mediante la ejecución de la instrucción SQL con todos los parámetros de la matriz con una sola llamada al origen de datos, esta funcionalidad no está ampliamente disponible en el DBMS hoy en día. Sin embargo, los controladores pueden simular mediante la ejecución de una instrucción SQL varias veces, cada uno con un único conjunto de parámetros.  
  
 Antes de que una aplicación utiliza matrices de parámetros, debe ser seguro de que son compatibles con los controladores utilizados por la aplicación. Hay dos formas de hacerlo:  
  
-   Use sólo los controladores que sabe que admiten las matrices de parámetros. La aplicación puede codificar los nombres de estos controladores, o puede pedirá al usuario que use solo estos controladores. Las aplicaciones personalizadas y aplicaciones verticales suelen usan un conjunto limitado de controladores.  
  
-   Comprobar la compatibilidad de las matrices de parámetros en tiempo de ejecución. Un controlador es compatible con matrices de parámetros si es posible establecer el atributo de instrucción de SQL_ATTR_PARAMSET_SIZE en un valor mayor que 1. Aplicaciones genéricas y aplicaciones verticales suelen comprobación la compatibilidad de las matrices de parámetros en tiempo de ejecución.  
  
 Se puede determinar la disponibilidad de los recuentos de filas y conjuntos de resultados en ejecución con parámetros mediante una llamada a **SQLGetInfo** con las opciones SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS. Para **insertar**, **actualización**, y **eliminar** instrucciones, la opción SQL_PARAM_ARRAY_ROW_COUNTS indica si son recuentos de filas individuales (uno para cada conjunto de parámetros) disponible (SQL_PARC_BATCH) o si se consolidan recuentos de filas en uno (SQL_PARC_NO_BATCH). Para **seleccione** instrucciones, la opción SQL_PARAM_ARRAY_SELECTS indica si un conjunto de resultados está disponible para cada conjunto de parámetros (SQL_PAS_BATCH) o si solo un conjunto de resultados está disponible (SQL_PAS_NO_BATCH). Si el controlador no admite las instrucciones generadora de conjunto de resultados que se ejecutarán con una matriz de parámetros, SQL_PARAM_ARRAY_SELECTS devuelve SQL_PAS_NO_SELECT. Si las matrices de parámetros se pueden utilizar con otros tipos de instrucciones, especialmente porque el uso de parámetros en estas instrucciones sería específicas del origen de datos y no seguir gramática SQL de ODBC es específica del origen de datos.  
  
 La matriz señalada por el atributo de instrucción SQL_ATTR_PARAM_OPERATION_PTR puede utilizarse para omitir las filas de parámetros. Si un elemento de la matriz se establece en SQL_PARAM_IGNORE, el conjunto de parámetros que corresponde a ese elemento se excluye de la **SQLExecute** o **SQLExecDirect** llamar. La matriz señalada por el atributo SQL_ATTR_PARAM_OPERATION_PTR es asignada y rellenada por la aplicación y leer el controlador. Si las filas capturadas se usan como parámetros de entrada, los valores de la matriz de Estados de fila pueden utilizarse en la matriz de parámetros de operación.  
  
## <a name="error-processing"></a>Procesamiento de errores  
 Si se produce un error al ejecutar la instrucción, la función de ejecución devuelve un error y establece la variable de número de fila en el número de la fila que contiene el error. Si todas las filas, salvo que se ejecute el conjunto de errores o si todas las filas antes de (pero no después) se ejecuta el conjunto de error es específico del origen de datos. Dado que procesa los conjuntos de parámetros, el controlador establece el búfer especificado por el atributo de instrucciones SQL_ATTR_PARAMS_PROCESSED_PTR para el número de la fila que se estaban procesando. Si todos los conjuntos, salvo que se ejecuta el conjunto de error, el controlador establece este búfer a SQL_ATTR_PARAMSET_SIZE después de que se procesan todas las filas.  
  
 Si se ha establecido el atributo de instrucciones SQL_ATTR_PARAM_STATUS_PTR, **SQLExecute** o **SQLExecDirect** devuelve el *matriz de Estados de parámetro,* que proporciona el estado de cada conjunto de parámetros. La matriz de Estados de parámetro es asignada por la aplicación y rellenada por el controlador. Sus elementos indican si se ha ejecutado correctamente la instrucción SQL para la fila de parámetros o si se produjo un error al procesar el conjunto de parámetros. Si se produjo un error, el controlador establece el valor correspondiente de la matriz de estado de parámetro para SQL_PARAM_ERROR y devuelve SQL_SUCCESS_WITH_INFO. La aplicación puede comprobar la matriz de estado para determinar qué filas se han procesado. Con el número de fila, la aplicación puede a menudo corregir el error y reanudar el procesamiento.  
  
 Uso de la matriz de Estados de parámetro viene determinada por las opciones de SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS devueltas por una llamada a **SQLGetInfo**. Para **insertar**, **actualización**, y **eliminar** instrucciones, la matriz de Estados de parámetro se rellena con información de estado si se devuelve SQL_PARC_BATCH para SQL_PARAM_ARRAY_ ROW_COUNTS, pero no si se devuelve SQL_PARC_NO_BATCH. Para **seleccione** instrucciones, la matriz de Estados de parámetro se rellena si se devuelve SQL_PAS_BATCH para SQL_PARAM_ARRAY_SELECT, pero no si se devuelve SQL_PAS_NO_BATCH o SQL_PAS_NO_SELECT.  
  
## <a name="data-at-execution-parameters"></a>Parámetros de datos en ejecución  
 Si alguno de los valores de la matriz de longitud/indicador SQL_DATA_AT_EXEC o el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro, los datos para esos valores se envían con **SQLPutData** de la forma habitual. Los siguientes aspectos de este proceso tenga comentario especial porque no son obvias de inmediato:  
  
-   Cuando el controlador devuelve SQL_NEED_DATA, se debe establecer la dirección de la variable de número de fila a la fila que necesita datos. Como se muestra en el caso de un solo valor, la aplicación no puede hacer ninguna suposición sobre el orden en que el controlador solicitará los valores de parámetro en un único conjunto de parámetros. Si se produce un error en la ejecución de un parámetro de datos en ejecución, el búfer especificado por el atributo de instrucciones SQL_ATTR_PARAMS_PROCESSED_PTR se establece en el número de la fila en el que se produjo el error, el estado de la fila de la matriz de Estados de fila especificada por se establece el atributo de instrucciones SQL_ATTR_PARAM_STATUS_PTR SQL_PARAM_ERROR y la llamada a **SQLExecute**, **SQLExecDirect**, **SQLParamData**, o  **SQLPutData** devuelve SQL_ERROR. El contenido de este búfer es indefinido si **SQLExecute**, **SQLExecDirect**, o **SQLParamData** devolver SQL_STILL_EXECUTING.  
  
-   Dado que el controlador no interpreta el valor de la *ParameterValuePtr* argumento de **SQLBindParameter** para los parámetros de datos en ejecución, si la aplicación proporciona un puntero a una matriz,  **SQLParamData** no extraer y devolver un elemento de esta matriz a la aplicación. En su lugar, devuelve que el valor escalar la aplicación tenía proporcionado. Esto significa que el valor devuelto por **SQLParamData** es no es suficiente para especificar el parámetro para el que la aplicación necesita para enviar datos; la aplicación también necesita tener en cuenta el número de fila actual.  
  
     Cuando sólo algunos de los elementos de una matriz de parámetros son parámetros de datos en ejecución, la aplicación debe pasar la dirección de una matriz en *ParameterValuePtr* que contiene los elementos para todos los parámetros. Esta matriz se interpreta normalmente para los parámetros que no son parámetros de datos en ejecución. Para los parámetros de datos en ejecución, el valor que **SQLParamData** proporciona a la aplicación, que normalmente podría usarse para identificar los datos que está solicitando el controlador en esta ocasión, siempre es la dirección de la matriz.
