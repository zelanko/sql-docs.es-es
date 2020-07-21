---
title: Varios resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d90414b631a7e81a7868ab7974b64ea84a0ea452
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302421"
---
# <a name="multiple-results"></a>Varios resultados
Un *resultado* es algo que devuelve el origen de datos después de ejecutar una instrucción. ODBC tiene dos tipos de resultados: conjuntos de resultados y recuentos de filas. Los *recuentos* de filas son el número de filas afectadas por una instrucción UPDATE, delete o INSERT. Los lotes, descritos en [lotes de instrucciones SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md), pueden generar varios resultados.  
  
 En la tabla siguiente se enumeran las opciones de **SQLGetInfo** que utiliza una aplicación para determinar si un origen de datos devuelve varios resultados para cada tipo de lote diferente. En concreto, un origen de datos puede devolver un recuento de filas único para todo el lote de instrucciones o recuentos de filas individuales para cada instrucción del lote. En el caso de una instrucción de generación de conjuntos de resultados que se ejecuta con una matriz de parámetros, el origen de datos puede devolver un único conjunto de resultados para todos los conjuntos de parámetros o conjuntos de resultados individuales para cada conjunto de parámetros.  
  
|Tipo de lote|Recuentos de filas|Conjuntos de resultados|  
|----------------|----------------|-----------------|  
|Lote explícito|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|Procedimiento|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|Matrices de parámetros|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] se puede admitir el número de filas que generan instrucciones en un lote, pero no se admite la devolución de los recuentos de filas. La opción SQL_BATCH_SUPPORT de **SQLGetInfo** indica si se permiten las instrucciones de generación de recuento de filas en los lotes; la opción SQL_BATCH_ROW_COUNTS indica si los recuentos de filas se devuelven a la aplicación.  
  
 [b] los lotes y procedimientos explícitos siempre devuelven varios conjuntos de resultados cuando incluyen varias instrucciones que generan conjuntos de resultados.  
  
> [!NOTE]  
>  La opción SQL_MULT_RESULT_SETS introducida en ODBC 1,0 solo proporciona información general sobre si se pueden devolver varios conjuntos de resultados. En concreto, se establece en "Y" si se devuelven los bits SQL_BS_SELECT_EXPLICIT o SQL_BS_SELECT_PROC para SQL_BATCH_SUPPORT o si se devuelve SQL_PAS_BATCH para SQL_PARAM_ARRAYS_SELECT.  
  
 Para procesar varios resultados, una aplicación llama a **SQLMoreResults**. Esta función descarta el resultado actual y hace que el resultado siguiente esté disponible. Devuelve SQL_NO_DATA cuando no hay más resultados disponibles. Por ejemplo, supongamos que las siguientes instrucciones se ejecutan como un lote:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Una vez ejecutadas estas instrucciones, la aplicación captura las filas del conjunto de resultados creado por la instrucción **Select** . Cuando ha terminado de capturar filas, llama a **SQLMoreResults** para poner a disposición el número de partes cuyo precio se ha reproducido. Si es necesario, **SQLMoreResults** descarta las filas no capturadas y cierra el cursor. A continuación, la aplicación llama a **SQLRowCount** para determinar el número de elementos que se recobran por la instrucción **Update** .  
  
 Es específico del controlador si toda la instrucción por lotes se ejecuta antes de que haya resultados disponibles. En algunas implementaciones, este es el caso; en otros, la llamada a **SQLMoreResults** desencadena la ejecución de la siguiente instrucción en el lote.  
  
 Si se produce un error en una de las instrucciones de un lote, **SQLMoreResults** devolverá SQL_ERROR o SQL_SUCCESS_WITH_INFO. Si se anuló el lote cuando se produjo un error en la instrucción o la instrucción con errores era la última instrucción del lote, **SQLMoreResults** devolverá SQL_ERROR. Si no se anuló el lote cuando se produjo un error en la instrucción y la instrucción errónea no era la última instrucción del lote, **SQLMoreResults** devolverá SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica que se ha generado al menos un conjunto de resultados o un recuento, y que no se ha anulado el lote.
