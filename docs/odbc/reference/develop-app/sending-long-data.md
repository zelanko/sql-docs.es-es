---
title: Enviar datos largos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc7a140d7de8548f02fde6ab309823bbe1c9c656
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465931"
---
# <a name="sending-long-data"></a>Enviar datos de tipo Long
Definen DBMS *datos long* como cualquier carácter o datos binarios a través de un determinado tamaño, por ejemplo, 254 caracteres. No sería posible almacenar un elemento de datos largos en memoria, como cuando el elemento representa un mapa de bits o un documento de texto largo. Porque no se puede almacenar estos datos en un único búfer, el origen de datos lo envía al controlador en partes con **SQLPutData** cuando se ejecuta la instrucción. Los parámetros para el que se envían los datos en tiempo de ejecución se conocen como *parámetros de datos en ejecución*.  
  
> [!NOTE]  
>  Una aplicación puede enviar cualquier tipo de datos en tiempo de ejecución con **SQLPutData**, aunque sólo caracteres y datos binarios pueden enviarse en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, normalmente hay ninguna razón para utilizar **SQLPutData**. Es mucho más fácil enlazar el búfer y dejar que el controlador de recuperar los datos desde el búfer.  
  
 Para enviar datos en tiempo de ejecución, la aplicación realiza las acciones siguientes:  
  
1.  Pasa un valor de 32 bits que identifica el parámetro en el *ParameterValuePtr* argumento en **SQLBindParameter** en lugar de pasar la dirección de un búfer. Este valor no se analizará el controlador. Se le devolverá a la aplicación más adelante, por lo que deben significar algo a la aplicación. Por ejemplo, podría ser el número del parámetro o el identificador de un archivo que contiene los datos.  
  
2.  Pasa la dirección de un búfer de longitud/indicador en el *StrLen_or_IndPtr* argumento de **SQLBindParameter**.  
  
3.  Almacena SQL_DATA_AT_EXEC o el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro en el búfer de longitud/indicador. Ambos de estos valores indican al controlador que se enviarán los datos para el parámetro con **SQLPutData**. SQL_LEN_DATA_AT_EXEC (*longitud*) se usa al enviar datos largos a un origen de datos que necesita saber cuántos bytes de datos largos se enviarán para que puede preasignar el espacio. Para determinar si un origen de datos necesita este valor, la aplicación llama a **SQLGetInfo** con la opción SQL_NEED_LONG_DATA_LEN. Todos los controladores deben admitir esta macro; Si el origen de datos no requiere la longitud en bytes, el controlador puede ignorarla.  
  
4.  Las llamadas **SQLExecute** o **SQLExecDirect**. El controlador detecta que un búfer de longitud/indicador contiene el valor SQL_DATA_AT_EXEC o el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro y devuelve SQL_NEED_DATA, como el valor devuelto de la función.  
  
5.  Las llamadas **SQLParamData** en respuesta a la SQL_NEED_DATA de valor devuelto. Si deben enviarse, datos de tipo long **SQLParamData** devuelve SQL_NEED_DATA. En el búfer señalado por el *ValuePtrPtr* argumento, el controlador devuelve el valor que identifica el parámetro de datos en ejecución. Si hay más de un parámetro de datos en ejecución, la aplicación debe utilizar este valor para determinar qué parámetro para enviar datos; el controlador no es necesario para solicitar datos de los parámetros de datos en ejecución en ningún orden concreto.  
  
6.  Las llamadas **SQLPutData** para enviar los datos del parámetro para el controlador. Si los datos del parámetro no caben en un único búfer, como suele ocurrir con datos de tipo long, la aplicación llama a **SQLPutData** varias veces para enviar los datos de partes; es hasta el origen de datos y el controlador para volver a ensamblar los datos. Si la aplicación pasa los datos de cadena terminada en null, el controlador u origen de datos debe quitar el carácter de terminación null como parte del proceso de reensamblado.  
  
7.  Las llamadas **SQLParamData** nuevo para indicar que ha enviado todos los datos para el parámetro. Si hay algún parámetro de datos en ejecución para el que no se han enviado datos, el controlador devuelve SQL_NEED_DATA y el valor que identifica el parámetro siguiente; la aplicación vuelve al paso 6. Si se ha enviado los datos para todos los parámetros de datos en ejecución, se ejecuta la instrucción. **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y puede devolver cualquier valor devuelto o diagnóstico que **SQLExecute** o **SQLExecDirect** puede devolver.  
  
 Después de **SQLExecute** o **SQLExecDirect** devuelve SQL_NEED_DATA y antes de datos se han enviado por completo para el último parámetro de datos en ejecución, la instrucción está en un estado de datos necesita. Mientras una instrucción está en un estado de datos necesita, la aplicación puede llamar solo **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, o **SQLGetDiagRec**; todas las demás funciones devuelven SQLSTATE HY010 (función de error de secuencia). Una llamada a **SQLCancel** cancela la ejecución de la instrucción y lo devuelve a su estado anterior. Para obtener más información, consulte [Apéndice B: Las tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obtener un ejemplo de envío de datos en tiempo de ejecución, consulte el [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) descripción de la función.
