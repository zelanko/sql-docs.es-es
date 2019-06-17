---
title: Datos de tipo Long y SQLSetPos y SQLBulkOperations | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d1a55d3b417ff7a0a673bda8d289a72d7c1cb1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312860"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Datos de tipo Long y SQLSetPos y SQLBulkOperations
Como sucede con los parámetros en instrucciones SQL, se pueden enviar datos largos al actualizar las filas con **SQLBulkOperations** o **SQLSetPos** o al insertar filas con **SQLBulkOperations**. Los datos se envían en partes, con varias llamadas a **SQLPutData**. Para que se envían los datos en tiempo de ejecución de las columnas se conocen como *columnas de datos en ejecución*.  
  
> [!NOTE]  
>  Una aplicación puede enviar cualquier tipo de datos en tiempo de ejecución con **SQLPutData**, aunque sólo caracteres y datos binarios pueden enviarse en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, normalmente hay ninguna razón para utilizar **SQLPutData**. Es mucho más fácil enlazar el búfer y dejar que el controlador de recuperar los datos desde el búfer.  
  
 Dado que las columnas de datos de tipo long no se enlazan normalmente, la aplicación debe enlazar la columna antes de llamar a **SQLBulkOperations** o **SQLSetPos** y desenlace después de llamar a **SQLBulkOperations**  o **SQLSetPos**. La columna debe estar enlazada porque **SQLBulkOperations** o **SQLSetPos** solo funciona en las columnas enlazadas y debe ser independiente para que **SQLGetData** puede usarse para recuperar datos en la columna.  
  
 Para enviar datos en tiempo de ejecución, la aplicación hace lo siguiente:  
  
1.  Coloca un valor de 32 bits en el búfer del conjunto de filas en lugar de un valor de datos. Este valor se devolverá a la aplicación más adelante, por lo que la aplicación debe establecer un valor significativo, como el número de la columna o el identificador de un archivo que contiene los datos.  
  
2.  Establece el valor en el búfer de longitud/indicador para el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro. Este valor indica al controlador que se enviarán los datos para el parámetro con **SQLPutData**. El *longitud* valor se usa al enviar datos largos a un origen de datos que necesita saber cuántos bytes de datos largos se enviarán para que puede preasignar el espacio. Para determinar si un origen de datos necesita este valor, la aplicación llama a **SQLGetInfo** con la opción SQL_NEED_LONG_DATA_LEN. Todos los controladores deben admitir esta macro; Si el origen de datos no requiere la longitud en bytes, el controlador puede ignorarla.  
  
3.  Las llamadas **SQLBulkOperations** o **SQLSetPos**. El controlador detecta que un búfer de longitud/indicador contiene el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro y devuelve SQL_NEED_DATA, como el valor devuelto de la función.  
  
4.  Las llamadas **SQLParamData** en respuesta a la SQL_NEED_DATA de valor devuelto. Si deben enviarse, datos de tipo long **SQLParamData** devuelve SQL_NEED_DATA. En el búfer señalado por el *ValuePtrPtr* argumento, el controlador devuelve el valor único que la aplicación se coloca en el búfer de conjunto de filas. Si hay más de una columna de datos en ejecución, la aplicación usa este valor para determinar la columna para enviar datos; el controlador no es necesario para solicitar datos de las columnas de datos en ejecución en ningún orden concreto.  
  
5.  Las llamadas **SQLPutData** para enviar los datos de columna para el controlador. Si los datos de columna no caben en un único búfer, como suele ocurrir con datos de tipo long, la aplicación llama a **SQLPutData** varias veces para enviar los datos de partes; es hasta el origen de datos y el controlador para volver a ensamblar los datos. Si la aplicación pasa los datos de cadena terminada en null, el controlador u origen de datos debe quitar el carácter de terminación null como parte del proceso de reensamblado.  
  
6.  Las llamadas **SQLParamData** nuevo para indicar que ha enviado todos los datos de la columna. Si hay columnas de datos en ejecución para el que no se han enviado datos, el controlador devuelve SQL_NEED_DATA y el valor único para la columna de datos en ejecución siguiente; la aplicación vuelve al paso 5. Si se ha enviado los datos para todas las columnas de datos en ejecución, los datos de la fila se envían al origen de datos. **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y puede devolver cualquier SQLSTATE **SQLBulkOperations** o **SQLSetPos** puede devolver.  
  
 Después de **SQLBulkOperations** o **SQLSetPos** devuelve SQL_NEED_DATA y antes de datos se han enviado por completo para la última columna de datos en ejecución, la instrucción está en un estado de datos necesita. En este estado, la aplicación puede llamar solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, o **SQLGetDiagRec**; todas las demás funciones devuelven SQLSTATE HY010 (función de error de secuencia). Una llamada a **SQLCancel** cancela la ejecución de la instrucción y lo devuelve a su estado anterior. Para obtener más información, consulte [Apéndice B: Las tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
