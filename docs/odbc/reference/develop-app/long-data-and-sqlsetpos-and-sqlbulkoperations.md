---
title: Datos de tipo Long y SQLSetPos y SQLBulkOperations | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 308e1ad6f2d99a0a6b7e73d8a82ac62362fea9a2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Datos de tipo Long y SQLSetPos y SQLBulkOperations
Como sucede con los parámetros en instrucciones SQL, se pueden enviar datos largos cuando actualizar filas con **SQLBulkOperations** o **SQLSetPos** o al insertar filas con **SQLBulkOperations**. Los datos se envían en partes, con varias llamadas a **SQLPutData**. Columnas para que se envían los datos en tiempo de ejecución se conocen como *columnas de datos en ejecución*.  
  
> [!NOTE]  
>  Una aplicación puede enviar cualquier tipo de datos en tiempo de ejecución con **SQLPutData**, aunque solo datos de caracteres y binarios se pueden enviar en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, no suele haber motivo para utilizar **SQLPutData**. Es mucho más fácil enlazar el búfer y dejar que el controlador de recuperar los datos desde el búfer.  
  
 Dado que las columnas de datos de tipo long no se enlazan normalmente, la aplicación debe enlazar la columna antes de llamar a **SQLBulkOperations** o **SQLSetPos** y desenlace después de llamar a **SQLBulkOperations ** o **SQLSetPos**. La columna debe estar enlazada porque **SQLBulkOperations** o **SQLSetPos** solo funciona en las columnas enlazadas y debe ser independiente para que **SQLGetData** puede usarse para recuperar datos en la columna.  
  
 Para enviar datos en tiempo de ejecución, la aplicación hace lo siguiente:  
  
1.  Coloca un valor de 32 bits en el búfer de conjunto de filas en lugar de un valor de datos. Este valor se devolverá a la aplicación más adelante, por lo que la aplicación debe establecer en un valor significativo, como el número de la columna o el identificador de un archivo que contiene los datos.  
  
2.  Establece el valor en el búfer de longitud/indicador en el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro. Este valor indica al controlador que enviará los datos para el parámetro con **SQLPutData**. El *longitud* valor se utiliza al enviar datos largos a un origen de datos que necesita conocer el número de bytes de datos largos se enviarán por lo que puede asignar previamente espacio. Para determinar si un origen de datos necesita este valor, la aplicación llama **SQLGetInfo** con la opción SQL_NEED_LONG_DATA_LEN. Todos los controladores deben admitir esta macro; Si el origen de datos no requiere la longitud en bytes, el controlador puede omitirla.  
  
3.  Llamadas **SQLBulkOperations** o **SQLSetPos**. El controlador detecta que un búfer de longitud/indicador contiene el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro y devuelve SQL_NEED_DATA como el valor devuelto de la función.  
  
4.  Llamadas **SQLParamData** en respuesta a la SQL_NEED_DATA de valor devuelto. Si deben enviarse, datos de tipo long **SQLParamData** devuelve SQL_NEED_DATA. En el búfer señalado por el *ValuePtrPtr* argumento, el controlador devuelve el valor único que la aplicación se coloca en el búfer de conjunto de filas. Si hay más de una columna de datos en ejecución, la aplicación usa este valor para determinar la columna que desea enviar los datos para; el controlador no es necesario para solicitar datos de las columnas de datos en ejecución en ningún orden concreto.  
  
5.  Llamadas **SQLPutData** para enviar los datos de columna para el controlador. Si los datos de columna no caben en un único búfer, como suele ocurrir con datos de tipo long, la aplicación llama a **SQLPutData** varias veces para enviar los datos en partes; depende de lo controladores y origen de datos para volver a ensamblar los datos. Si la aplicación pasa los datos de cadena terminada en null, el controlador u origen de datos debe quitar el carácter de terminación null como parte del proceso de volver a ensamblar.  
  
6.  Llamadas **SQLParamData** nuevo para indicar que ha enviado todos los datos de la columna. Si no hay ninguna columna de datos en ejecución para el que no se han enviado datos, el controlador devuelve SQL_NEED_DATA y el valor único de la columna de datos en ejecución siguiente: la aplicación vuelve al paso 5. Si se han enviado datos para todas las columnas de datos en ejecución, los datos de la fila se envían al origen de datos. **SQLParamData** , a continuación, devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y puede devolver cualquier SQLSTATE **SQLBulkOperations** o **SQLSetPos** puede devolver.  
  
 Después de **SQLBulkOperations** o **SQLSetPos** devuelve SQL_NEED_DATA y antes de que se han enviado datos completamente para la última columna de datos en ejecución, la instrucción se encuentra en un estado de datos necesita. En este estado, la aplicación puede llamar a solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, o **SQLGetDiagRec**; todas las demás funciones devuelven SQLSTATE HY010 (error de secuencia de función). Al llamar a **SQLCancel** cancela la ejecución de la instrucción y lo devuelve a su estado anterior. Para obtener más información, consulte [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
