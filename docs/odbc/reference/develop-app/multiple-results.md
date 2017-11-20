---
title: Varios resultados | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62a4b7edd47ca6c9a6b1c7469e18269af3ab907d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="multiple-results"></a>Varios resultados
A *resultado* algo devuelto por el origen de datos después de ejecutar una instrucción. ODBC tiene dos tipos de resultados: conjuntos de resultados y recuento de filas. *Recuento de filas* son el número de filas afectadas por una instrucción update, delete o insert instrucción. Lotes, se describe en [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md), puede generar varios resultados.  
  
 La siguiente tabla se recogen los **SQLGetInfo** opciones de una aplicación que se usa para determinar si un origen de datos devuelve varios resultados para cada tipo de lote diferente. En concreto, un origen de datos puede devolver un recuento de filas único para todo el lote de instrucciones o recuento de filas individuales para cada instrucción del lote. En el caso de los resultados: Generar conjunto ejecutada una instrucción con una matriz de parámetros, el origen de datos puede devolver un único conjunto de resultados para todos los conjuntos de parámetros o conjuntos de resultados individuales para cada conjunto de parámetros.  
  
|Tipo de lote|Recuentos de filas|Conjuntos de resultados|  
|----------------|----------------|-----------------|  
|Explícito de lotes|SQL_BATCH_ROW_COUNT [a]|--[b].|  
|Procedimiento|SQL_BATCH_ROW_COUNT [a]|--[b].|  
|Matrices de parámetros|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 no admite [a] fila pueden admitirse recuento: generar instrucciones en un lote, pero la devolución de los recuentos de filas. La opción SQL_BATCH_SUPPORT en **SQLGetInfo** indica si se permiten las instrucciones de generación de recuento de filas en lotes; la opción SQL_BATCH_ROW_COUNTS indica si estos recuentos de filas se devuelven a la aplicación.  
  
 [b] lotes explícitos y procedimientos siempre devuelven varios conjuntos de resultados cuando incluyen varias instrucciones de generación de conjunto de resultados.  
  
> [!NOTE]  
>  La opción SQL_MULT_RESULT_SETS introducida en ODBC 1.0 proporciona información general solo sobre si se pueden devolver varios conjuntos de resultados. En concreto, se establece en "Y" si se devuelven los bits SQL_BS_SELECT_EXPLICIT o SQL_BS_SELECT_PROC para SQL_BATCH_SUPPORT o si se devuelve SQL_PAS_BATCH para SQL_PARAM_ARRAYS_SELECT.  
  
 Para procesar varios resultados, una aplicación llama **SQLMoreResults**. Esta función descarta el resultado actual y pone a disposición el resultado siguiente. Devuelve SQL_NO_DATA cuando no hay más resultados disponibles. Por ejemplo, suponga que las siguientes instrucciones se ejecutan como un lote:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Después de que se ejecutan estas instrucciones, la aplicación captura filas del conjunto de resultados creado por el **seleccione** instrucción. Cuando se hizo captura filas, llama al método **SQLMoreResults** para que esté disponible el número de elementos que se han repriced. Si es necesario, **SQLMoreResults** descarta las filas no recuperadas y cierra el cursor. A continuación, la aplicación llama a **SQLRowCount** para determinar cuántos elementos se repriced por el **actualización** instrucción.  
  
 Es específica del controlador si se ejecuta la instrucción del lote completo antes de que todos los resultados estén disponibles. En algunas implementaciones, este es el caso; en otros casos, al llamar a **SQLMoreResults** desencadena la ejecución de la siguiente instrucción del lote.  
  
 Si se produce un error en una de las instrucciones en un lote, **SQLMoreResults** devolverá SQL_ERROR o SQL_SUCCESS_WITH_INFO. Si se anula el lote al error de la instrucción o la instrucción con errores era la última instrucción del lote, **SQLMoreResults** devolverá SQL_ERROR. Si no se anula el lote al error de la instrucción y la instrucción con errores no era la última instrucción del lote, **SQLMoreResults** devuelve SQL_SUCCESS_WITH_INFO. SQL_SUCCESS_WITH_INFO indica que se generó al menos un conjunto de resultados o recuento y que no se anuló el lote.

