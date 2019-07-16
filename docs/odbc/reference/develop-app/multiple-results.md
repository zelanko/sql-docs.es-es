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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8679bea49b63ffd5dc7164942b42ac9eed7e9ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086360"
---
# <a name="multiple-results"></a>Varios resultados
Un *resultado* algo devuelto por el origen de datos después de ejecutar una instrucción. ODBC tiene dos tipos de resultados: conjuntos de resultados y recuentos de filas. *Recuento de filas* son el número de filas afectadas por una actualización, eliminación o instrucción insert. Los lotes, se describe en [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md), puede generar varios resultados.  
  
 La siguiente tabla se enumeran los **SQLGetInfo** opciones de una aplicación que se utiliza para determinar si un origen de datos devuelve varios resultados para cada tipo de lote diferente. En concreto, un origen de datos puede devolver un recuento de filas único para todo el lote de instrucciones o cantidad de filas individuales de cada instrucción del lote. En el caso de una instrucción de generación de conjunto de la resultado ejecutada con una matriz de parámetros, el origen de datos puede devolver un único conjunto de resultados para todos los conjuntos de parámetros o conjuntos de resultados individuales para cada conjunto de parámetros.  
  
|Tipo de lote|Recuentos de filas|Conjuntos de resultados|  
|----------------|----------------|-----------------|  
|Explícito de lotes|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|Procedimiento|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|Matrices de parámetros|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] fila pueden admitir la generación de recuento de instrucciones en un lote, aunque la devolución de los recuentos de filas no admite. La opción SQL_BATCH_SUPPORT en **SQLGetInfo** indica si se permiten las instrucciones de generación de recuento de filas en lotes; la opción SQL_BATCH_ROW_COUNTS indica si estos recuentos de filas se devuelven a la aplicación.  
  
 [b] lotes explícitos y procedimientos siempre devuelven varios conjuntos de resultados cuando incluyen varias instrucciones de generación de conjunto de resultados.  
  
> [!NOTE]  
>  La opción SQL_MULT_RESULT_SETS introducida en ODBC 1.0 proporciona información general solo sobre si se pueden devolver varios conjuntos de resultados. En concreto, se establece en "Y" si se devuelven los bits SQL_BS_SELECT_EXPLICIT o SQL_BS_SELECT_PROC para SQL_BATCH_SUPPORT o si se devuelve SQL_PAS_BATCH para SQL_PARAM_ARRAYS_SELECT.  
  
 Para procesar varios resultados, una aplicación llama a **SQLMoreResults**. Esta función descarta el resultado actual y pone a disposición el resultado siguiente. Devuelve SQL_NO_DATA cuando no hay más resultados disponibles. Por ejemplo, suponga que las siguientes instrucciones se ejecutan como un lote:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Después de que se ejecuten estas instrucciones, la aplicación captura las filas del conjunto de resultados creado por el **seleccione** instrucción. Cuando termine capturar filas, llama a **SQLMoreResults** para que esté disponible el número de elementos que se han repriced. Si es necesario, **SQLMoreResults** descarta las filas no recuperadas y cierra el cursor. La aplicación, a continuación, llama a **SQLRowCount** para determinar cuántos elementos se repriced por el **actualización** instrucción.  
  
 Es específico del controlador si se ejecuta la instrucción del lote completo para que los resultados estén disponibles. En algunas implementaciones, este es el caso; en otros casos, una llamada a **SQLMoreResults** desencadena la ejecución de la siguiente instrucción del lote.  
  
 Si se produce un error en una de las instrucciones en un lote, **SQLMoreResults** devolverá SQL_ERROR o SQL_SUCCESS_WITH_INFO. Si se anuló el lote al error de la instrucción o la instrucción con errores era la última instrucción del lote, **SQLMoreResults** devolverá SQL_ERROR. Si no se anuló el lote al error de la instrucción y la instrucción con errores no era la última instrucción del lote, **SQLMoreResults** devolverá SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica que se generó al menos un conjunto de resultados o de recuento y que no se anuló el lote.
