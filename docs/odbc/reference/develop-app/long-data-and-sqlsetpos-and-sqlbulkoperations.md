---
title: Long Data y SQLSetPos y SQLBulkOperations | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287869"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Datos de tipo Long y SQLSetPos y SQLBulkOperations
Como ocurre con los parámetros de las instrucciones SQL, se pueden enviar datos largos al actualizar filas con **SQLBulkOperations** o **SQLSetPos** , o al insertar filas con **SQLBulkOperations**. Los datos se envían en partes, con varias llamadas a **SQLPutData**. Las columnas para las que se envían datos en tiempo de ejecución se denominan *columnas de datos en ejecución*.  
  
> [!NOTE]  
>  En realidad, una aplicación puede enviar cualquier tipo de datos en tiempo de ejecución con **SQLPutData**, aunque solo los datos de caracteres y binarios se pueden enviar en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un solo búfer, generalmente no hay ningún motivo para usar **SQLPutData**. Es mucho más fácil enlazar el búfer y dejar que el controlador recupere los datos del búfer.  
  
 Dado que las columnas de datos largas no se enlazan normalmente, la aplicación debe enlazar la columna antes de llamar a **SQLBulkOperations** o **SQLSetPos** y desenlazarla después de llamar a **SQLBulkOperations** o **SQLSetPos**. La columna debe estar enlazada porque **SQLBulkOperations** o **SQLSetPos** solo funcionan en columnas enlazadas y deben estar sin enlazar para que se pueda usar **SQLGetData** para recuperar datos de la columna.  
  
 Para enviar datos en tiempo de ejecución, la aplicación hace lo siguiente:  
  
1.  Coloca un valor de 32 bits en el búfer del conjunto de filas en lugar de un valor de datos. Este valor se devolverá a la aplicación más adelante, por lo que la aplicación debe establecerlo en un valor significativo, como el número de la columna o el identificador de un archivo que contiene datos.  
  
2.  Establece el valor del búfer de longitud/indicador en el resultado de la macro SQL_LEN_DATA_AT_EXEC (*longitud*). Este valor indica al controlador que los datos para el parámetro se enviarán con **SQLPutData**. El valor de *longitud* se usa al enviar datos largos a un origen de datos que necesita saber cuántos bytes de datos largos se enviarán para que pueda asignar espacio previamente. Para determinar si un origen de datos requiere este valor, la aplicación llama a **SQLGetInfo** con la opción SQL_NEED_LONG_DATA_LEN. Todos los controladores deben admitir esta macro; Si el origen de datos no requiere la longitud de bytes, el controlador puede pasarlo por alto.  
  
3.  Llama a **SQLBulkOperations** o **SQLSetPos**. El controlador detecta que un búfer de longitud/indicador contiene el resultado de la macro SQL_LEN_DATA_AT_EXEC (*longitud*) y devuelve SQL_NEED_DATA como el valor devuelto de la función.  
  
4.  Llama a **SQLParamData** en respuesta a la SQL_NEED_DATA valor devuelto. Si es necesario enviar datos largos, **SQLParamData** devuelve SQL_NEED_DATA. En el búfer señalado por el argumento *ValuePtrPtr* , el controlador devuelve el valor único que la aplicación colocó en el búfer del conjunto de filas. Si hay más de una columna de datos en ejecución, la aplicación usa este valor para determinar la columna para la que se van a enviar datos; no es necesario que el controlador solicite datos para las columnas de datos en ejecución en un orden determinado.  
  
5.  Llama a **SQLPutData** para enviar los datos de columna al controlador. Si los datos de la columna no caben en un solo búfer, como suele ser el caso de datos Long, la aplicación llama a **SQLPutData** varias veces para enviar los datos en partes; depende del controlador y del origen de datos volver a ensamblar los datos. Si la aplicación pasa datos de cadena terminada en null, el controlador o el origen de datos debe quitar el carácter de terminación NULL como parte del proceso de reensamblado.  
  
6.  Llama de nuevo a **SQLParamData** para indicar que se han enviado todos los datos de la columna. Si hay columnas de datos en ejecución para las que no se han enviado datos, el controlador devuelve SQL_NEED_DATA y el valor único de la siguiente columna de datos en ejecución; la aplicación vuelve al paso 5. Si se han enviado datos para todas las columnas de datos en ejecución, los datos de la fila se envían al origen de datos. A continuación, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y puede devolver cualquier SQLSTATE que **SQLBulkOperations** o **SQLSetPos** pueda devolver.  
  
 Después de que **SQLBulkOperations** o **SQLSetPos** devuelvan SQL_NEED_DATA y antes de que los datos se hayan enviado completamente para la última columna de datos en ejecución, la instrucción se encuentra en un estado de necesidad de datos. En este estado, la aplicación solo puede llamar a **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**o **SQLGetDiagRec**; todas las demás funciones devuelven SQLSTATE HY010 (error de secuencia de función). Al llamar a **SQLCancel** se cancela la ejecución de la instrucción y se devuelve a su estado anterior. Para obtener más información, vea el [Apéndice B: tablas de transición de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
