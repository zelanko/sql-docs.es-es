---
title: Envío de datos largos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aeeeb716aa2f9a72338f3aeb586dffce86f84069
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304186"
---
# <a name="sending-long-data"></a>Enviar datos de tipo Long
Los DBMS definen *datos largos* como cualquier carácter o datos binarios de un tamaño determinado, como 254 caracteres. Es posible que no sea posible almacenar un elemento completo de datos largos en la memoria, como cuando el elemento representa un documento de texto largo o un mapa de bits. Dado que estos datos no se pueden almacenar en un único búfer, el origen de datos los envía al controlador en partes con **SQLPutData** cuando se ejecuta la instrucción. Los parámetros para los que se envían datos en tiempo de ejecución se conocen como *parámetros de datos en ejecución.*  
  
> [!NOTE]  
>  Una aplicación puede enviar realmente cualquier tipo de datos en tiempo de ejecución con **SQLPutData**, aunque solo los datos binarios y de caracteres se pueden enviar en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, generalmente no hay ninguna razón para usar **SQLPutData**. Es mucho más fácil enlazar el búfer y dejar que el controlador recupere los datos del búfer.  
  
 Para enviar datos en tiempo de ejecución, la aplicación realiza las siguientes acciones:  
  
1.  Pasa un valor de 32 bits que identifica el parámetro en el *ParameterValuePtr* argumento en **SQLBindParameter** en lugar de pasar la dirección de un búfer. El controlador no analiza este valor. Se devolverá a la aplicación más adelante, por lo que debe significar algo para la aplicación. Por ejemplo, podría ser el número del parámetro o el identificador de un archivo que contiene datos.  
  
2.  Pasa la dirección de un búfer de longitud/indicador en el argumento *StrLen_or_IndPtr* de **SQLBindParameter**.  
  
3.  Almacena SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*) en el búfer de longitud/indicador. Ambos valores indican al controlador que los datos del parámetro se enviarán con **SQLPutData**. SQL_LEN_DATA_AT_EXEC(*longitud*) se utiliza al enviar datos largos a un origen de datos que necesita saber cuántos bytes de datos largos se enviarán para que pueda preasignar espacio. Para determinar si un origen de datos requiere este valor, la aplicación llama a **SQLGetInfo** con la opción SQL_NEED_LONG_DATA_LEN. Todos los controladores deben admitir esta macro; si el origen de datos no requiere la longitud del byte, el controlador puede ignorarlo.  
  
4.  Llama a **SQLExecute** o **SQLExecDirect**. El controlador descubre que un búfer de longitud/indicador contiene el valor SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*) y devuelve SQL_NEED_DATA como valor devuelto de la función.  
  
5.  Llama a **SQLParamData** en respuesta al valor devuelto SQL_NEED_DATA. Si es necesario enviar datos largos, **SQLParamData** devuelve SQL_NEED_DATA. En el búfer al que apunta el *ValuePtrPtr* argumento, el controlador devuelve el valor que identifica el parámetro de datos en ejecución. Si hay más de un parámetro de datos en ejecución, la aplicación debe usar este valor para determinar para qué parámetro enviar datos; el controlador no es necesario para solicitar datos para los parámetros de datos en ejecución en un orden determinado.  
  
6.  Llama a **SQLPutData** para enviar los datos de parámetro al controlador. Si los datos de parámetro no caben en un único búfer, como suele ocurrir con los datos largos, la aplicación llama a **SQLPutData** repetidamente para enviar los datos en partes; depende del controlador y del origen de datos volver a ensamblar los datos. Si la aplicación pasa datos de cadena terminados en null, el controlador o el origen de datos debe quitar el carácter de terminación nula como parte del proceso de reensamblado.  
  
7.  Llama a **SQLParamData** de nuevo para indicar que ha enviado todos los datos para el parámetro. Si hay parámetros de datos en ejecución para los que no se han enviado datos, el controlador devuelve SQL_NEED_DATA y el valor que identifica el siguiente parámetro; la aplicación vuelve al paso 6. Si se han enviado datos para todos los parámetros de datos en ejecución, se ejecuta la instrucción. **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y puede devolver cualquier valor devuelto o diagnóstico que **SQLExecute** o **SQLExecDirect** puede devolver.  
  
 Después de **SQLExecute** o **SQLExecDirect** devuelve SQL_NEED_DATA y antes de que los datos se hayan enviado completamente para el último parámetro de datos en ejecución, la instrucción está en un estado Need Data. Mientras una instrucción está en un estado Need Data, la aplicación solo puede llamar a **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**o **SQLGetDiagRec**; todas las demás funciones devuelven SQLSTATE HY010 (error de secuencia de funciones). Al llamar a **SQLCancel** se cancela la ejecución de la instrucción y se devuelve a su estado anterior. Para obtener más información, vea [Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .  
  
 Para obtener un ejemplo de envío de datos en tiempo de ejecución, vea la descripción de la función [SQLPutData.](../../../odbc/reference/syntax/sqlputdata-function.md)
