---
title: Enviando datos largos | Microsoft Docs
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
ms.openlocfilehash: acb4ff1637c1530527af88affaf437334596016b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094342"
---
# <a name="sending-long-data"></a>Enviar datos de tipo Long
Los DBMS definen *datos largos* como cualquier carácter o dato binario a lo largo de un determinado tamaño, como 254 caracteres. Es posible que no sea posible almacenar un elemento completo de datos largos en memoria, como cuando el elemento representa un documento de texto largo o un mapa de bits. Dado que estos datos no se pueden almacenar en un solo búfer, el origen de datos lo envía al controlador en partes con **SQLPutData** cuando se ejecuta la instrucción. Los parámetros para los que se envían los datos en tiempo de ejecución se conocen como *parámetros de datos en ejecución*.  
  
> [!NOTE]  
>  En realidad, una aplicación puede enviar cualquier tipo de datos en tiempo de ejecución con **SQLPutData**, aunque solo los datos de caracteres y binarios se pueden enviar en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un solo búfer, generalmente no hay ningún motivo para usar **SQLPutData**. Es mucho más fácil enlazar el búfer y dejar que el controlador recupere los datos del búfer.  
  
 Para enviar datos en tiempo de ejecución, la aplicación realiza las siguientes acciones:  
  
1.  Pasa un valor de 32 bits que identifica el parámetro en el argumento *ParameterValuePtr* en **SQLBindParameter** en lugar de pasar la dirección de un búfer. El controlador no analiza este valor. Se devolverá a la aplicación más adelante, por lo que debe significar algo a la aplicación. Por ejemplo, podría ser el número del parámetro o el identificador de un archivo que contiene datos.  
  
2.  Pasa la dirección de un búfer de longitud/indicador en el argumento *StrLen_or_IndPtr* de **SQLBindParameter**.  
  
3.  Almacena SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC (*length*) en el búfer de longitud/indicador. Ambos valores indican al controlador que los datos para el parámetro se enviarán con **SQLPutData**. SQL_LEN_DATA_AT_EXEC (*longitud*) se usa al enviar datos largos a un origen de datos que necesita saber el número de bytes de datos largos que se enviarán para que pueda asignar espacio previamente. Para determinar si un origen de datos requiere este valor, la aplicación llama a **SQLGetInfo** con la opción SQL_NEED_LONG_DATA_LEN. Todos los controladores deben admitir esta macro; Si el origen de datos no requiere la longitud de bytes, el controlador puede pasarlo por alto.  
  
4.  Llama a **SQLExecute** o **SQLExecDirect**. El controlador detecta que un búfer de longitud/indicador contiene el valor SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC (*longitud*) y devuelve SQL_NEED_DATA como valor devuelto de la función.  
  
5.  Llama a **SQLParamData** en respuesta a la SQL_NEED_DATA valor devuelto. Si es necesario enviar datos largos, **SQLParamData** devuelve SQL_NEED_DATA. En el búfer señalado por el argumento *ValuePtrPtr* , el controlador devuelve el valor que identifica el parámetro de datos en ejecución. Si hay más de un parámetro de datos en ejecución, la aplicación debe usar este valor para determinar el parámetro para el que se van a enviar datos; no es necesario que el controlador solicite datos para los parámetros de datos en ejecución en un orden determinado.  
  
6.  Llama a **SQLPutData** para enviar los datos del parámetro al controlador. Si los datos del parámetro no caben en un solo búfer, como suele ser el caso de los datos de tipo Long, la aplicación llama a **SQLPutData** varias veces para enviar los datos en partes; depende del controlador y del origen de datos volver a ensamblar los datos. Si la aplicación pasa datos de cadena terminada en null, el controlador o el origen de datos debe quitar el carácter de terminación NULL como parte del proceso de reensamblado.  
  
7.  Llama de nuevo a **SQLParamData** para indicar que se han enviado todos los datos para el parámetro. Si hay parámetros de datos en ejecución para los que no se han enviado datos, el controlador devuelve SQL_NEED_DATA y el valor que identifica el parámetro siguiente; la aplicación vuelve al paso 6. Si se han enviado datos para todos los parámetros de datos en ejecución, se ejecuta la instrucción. **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y puede devolver cualquier valor devuelto o diagnóstico que puede devolver **SQLExecute** o **SQLExecDirect** .  
  
 Después de que **SQLExecute** o **SQLExecDirect** devuelva SQL_NEED_DATA y antes de que los datos se hayan enviado completamente para el último parámetro de datos en ejecución, la instrucción se encuentra en un estado de necesidad de datos. Mientras que una instrucción está en un estado de datos necesario, la aplicación solo puede llamar a **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**o **SQLGetDiagRec**; todas las demás funciones devuelven SQLSTATE HY010 (error de secuencia de función). Al llamar a **SQLCancel** se cancela la ejecución de la instrucción y se devuelve a su estado anterior. Para obtener más información, vea el [Apéndice B: tablas de transición de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obtener un ejemplo de envío de datos en tiempo de ejecución, vea la descripción de la función [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) .
