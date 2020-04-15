---
title: Datos largos y SQLSetPos y SQLBulkOperations Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bc6c5d2da2f796a7c312971635fc36bc2fae8af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287869"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Datos de tipo Long y SQLSetPos y SQLBulkOperations
Como es el caso con los parámetros de las instrucciones SQL, se pueden enviar datos largos al actualizar filas con **SQLBulkOperations** o **SQLSetPos** o al insertar filas con **SQLBulkOperations**. Los datos se envían en partes, con varias llamadas a **SQLPutData**. Las columnas para las que se envían datos en tiempo de ejecución se conocen como *columnas de datos en ejecución.*  
  
> [!NOTE]  
>  Una aplicación realmente puede enviar cualquier tipo de datos en tiempo de ejecución con **SQLPutData**, aunque solo los datos binarios y de caracteres se pueden enviar en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, generalmente no hay ninguna razón para usar **SQLPutData**. Es mucho más fácil enlazar el búfer y dejar que el controlador recupere los datos del búfer.  
  
 Dado que las columnas de datos largos normalmente no están enlazadas, la aplicación debe enlazar la columna antes de llamar a **SQLBulkOperations** o **SQLSetPos** y desvincularla después de llamar a **SQLBulkOperations** o **SQLSetPos**. La columna debe enlazarse porque **SQLBulkOperations** o **SQLSetPos** solo funciona en columnas enlazadas y debe estar desenlazada para que **SQLGetData** se pueda usar para recuperar datos de la columna.  
  
 Para enviar datos en tiempo de ejecución, la aplicación hace lo siguiente:  
  
1.  Coloca un valor de 32 bits en el búfer del conjunto de filas en lugar de un valor de datos. Este valor se devolverá a la aplicación más adelante, por lo que la aplicación debe establecerlo en un valor significativo, como el número de la columna o el identificador de un archivo que contiene datos.  
  
2.  Establece el valor del búfer de longitud/indicador en el resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*). Este valor indica al controlador que los datos del parámetro se enviarán con **SQLPutData**. El valor *de longitud* se utiliza al enviar datos largos a un origen de datos que necesita saber cuántos bytes de datos largos se enviarán para que pueda preasignar espacio. Para determinar si un origen de datos requiere este valor, la aplicación llama a **SQLGetInfo** con la opción SQL_NEED_LONG_DATA_LEN. Todos los controladores deben admitir esta macro; si el origen de datos no requiere la longitud del byte, el controlador puede ignorarlo.  
  
3.  Llama a **SQLBulkOperations** o **SQLSetPos**. El controlador descubre que un búfer de longitud/indicador contiene el resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*) y devuelve SQL_NEED_DATA como el valor devuelto de la función.  
  
4.  Llama a **SQLParamData** en respuesta al valor devuelto SQL_NEED_DATA. Si es necesario enviar datos largos, **SQLParamData** devuelve SQL_NEED_DATA. En el búfer al que apunta el *ValuePtrPtr* argumento, el controlador devuelve el valor único que la aplicación colocó en el búfer de conjunto de filas. Si hay más de una columna de datos en ejecución, la aplicación utiliza este valor para determinar para qué columna enviar datos; el controlador no es necesario para solicitar datos para las columnas de datos en ejecución en un orden determinado.  
  
5.  Llama a **SQLPutData** para enviar los datos de columna al controlador. Si los datos de columna no caben en un único búfer, como suele ocurrir con los datos largos, la aplicación llama a **SQLPutData** repetidamente para enviar los datos en partes; depende del controlador y del origen de datos volver a ensamblar los datos. Si la aplicación pasa datos de cadena terminados en null, el controlador o el origen de datos debe quitar el carácter de terminación nula como parte del proceso de reensamblado.  
  
6.  Llama a **SQLParamData** de nuevo para indicar que ha enviado todos los datos de la columna. Si hay columnas de datos en ejecución para las que no se han enviado datos, el controlador devuelve SQL_NEED_DATA y el valor único para la siguiente columna de datos en ejecución; la aplicación vuelve al paso 5. Si se han enviado datos para todas las columnas de datos en ejecución, los datos de la fila se envían al origen de datos. **SQLParamData,** a continuación, devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y puede devolver cualquier SQLSTATE que **SQLBulkOperations** o **SQLSetPos** puede devolver.  
  
 Después de **SQLBulkOperations** o **SQLSetPos** devuelve SQL_NEED_DATA y antes de que los datos se hayan enviado completamente para la última columna de datos en ejecución, la instrucción está en un estado De necesidad de datos. En este estado, la aplicación solo puede llamar a **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**o **SQLGetDiagRec**; todas las demás funciones devuelven SQLSTATE HY010 (error de secuencia de funciones). Al llamar a **SQLCancel** se cancela la ejecución de la instrucción y se devuelve a su estado anterior. Para obtener más información, vea [Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .
