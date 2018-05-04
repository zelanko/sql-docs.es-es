---
title: Enviar datos de tipo Long | Documentos de Microsoft
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
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 260c62d849f1b771b6d9fc40245fd1b0bfd2c5ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sending-long-data"></a>Enviar datos de tipo Long
Definen DBMS *datos long* como cualquier carácter o datos binarios a través de un determinado tamaño, como 254 caracteres. No sería posible almacenar un elemento de datos largos en memoria, como cuando el elemento representa un mapa de bits o un documento de texto largo. Porque no se puede almacenar estos datos en un único búfer, el origen de datos lo envía al controlador en partes con **SQLPutData** cuando se ejecuta la instrucción. Parámetros para la que se envían los datos en tiempo de ejecución se conocen como *parámetros de datos en ejecución*.  
  
> [!NOTE]  
>  Una aplicación puede enviar cualquier tipo de datos en tiempo de ejecución con **SQLPutData**, aunque solo datos de caracteres y binarios se pueden enviar en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, no suele haber motivo para utilizar **SQLPutData**. Es mucho más fácil enlazar el búfer y dejar que el controlador de recuperar los datos desde el búfer.  
  
 Para enviar datos en tiempo de ejecución, la aplicación realiza las siguientes acciones:  
  
1.  Pasa un valor de 32 bits que identifica el parámetro en el *ParameterValuePtr* argumento en **SQLBindParameter** en lugar de pasar la dirección de un búfer. Este valor no se analiza el controlador. Se devolverá a la aplicación más adelante, por lo que debe significa algo a la aplicación. Por ejemplo, sería el número del parámetro o el identificador de un archivo que contiene los datos.  
  
2.  Pasa la dirección de un búfer de longitud/indicador en el *StrLen_or_IndPtr* argumento de **SQLBindParameter**.  
  
3.  Almacena SQL_DATA_AT_EXEC o el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro en el búfer de longitud/indicador. Estos dos valores indican al controlador que enviará los datos para el parámetro con **SQLPutData**. SQL_LEN_DATA_AT_EXEC (*longitud*) se usa al enviar datos largos a un origen de datos que necesita conocer el número de bytes de datos largos se enviarán por lo que puede asignar previamente espacio. Para determinar si un origen de datos necesita este valor, la aplicación llama a **SQLGetInfo** con la opción SQL_NEED_LONG_DATA_LEN. Todos los controladores deben admitir esta macro; Si el origen de datos no requiere la longitud en bytes, el controlador puede omitirla.  
  
4.  Llamadas **SQLExecute** o **SQLExecDirect**. El controlador detecta que un búfer de longitud/indicador contiene el valor SQL_DATA_AT_EXEC o el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro y devuelve SQL_NEED_DATA como el valor devuelto de la función.  
  
5.  Llamadas **SQLParamData** en respuesta a la SQL_NEED_DATA de valor devuelto. Si deben enviarse, datos de tipo long **SQLParamData** devuelve SQL_NEED_DATA. En el búfer señalado por el *ValuePtrPtr* argumento, el controlador devuelve el valor que identifica el parámetro de datos en ejecución. Si hay más de un parámetro de datos en ejecución, la aplicación debe utilizar este valor para determinar qué parámetro para enviar datos; el controlador no es necesario para solicitar datos de los parámetros de datos en ejecución en ningún orden concreto.  
  
6.  Llamadas **SQLPutData** para enviar los datos del parámetro del controlador. Si los datos del parámetro no caber en un único búfer, como suele ocurrir con datos de tipo long, la aplicación llama a **SQLPutData** varias veces para enviar los datos en partes; depende de lo controladores y origen de datos para volver a ensamblar los datos. Si la aplicación pasa los datos de cadena terminada en null, el controlador u origen de datos debe quitar el carácter de terminación null como parte del proceso de volver a ensamblar.  
  
7.  Llamadas **SQLParamData** nuevo para indicar que ha enviado todos los datos para el parámetro. Si hay algún parámetro de datos en ejecución para el que no se han enviado datos, el controlador devuelve SQL_NEED_DATA y el valor que identifica el parámetro siguiente; la aplicación vuelve al paso 6. Si se han enviado datos para todos los parámetros de datos en ejecución, se ejecuta la instrucción. **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y puede devolver cualquier valor devuelto o diagnóstico que **SQLExecute** o **SQLExecDirect** puede devolver.  
  
 Después de **SQLExecute** o **SQLExecDirect** devuelve SQL_NEED_DATA y antes de que se han enviado datos completamente para el último parámetro de datos en ejecución, la instrucción se encuentra en un estado de datos necesita. Mientras una instrucción está en un estado de datos necesita, la aplicación puede llamar a solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, o **SQLGetDiagRec**; todas las demás funciones devuelven SQLSTATE HY010 (error de secuencia de función). Al llamar a **SQLCancel** cancela la ejecución de la instrucción y lo devuelve a su estado anterior. Para obtener más información, consulte [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obtener un ejemplo de envío de datos en tiempo de ejecución, consulte el [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) descripción de la función.
