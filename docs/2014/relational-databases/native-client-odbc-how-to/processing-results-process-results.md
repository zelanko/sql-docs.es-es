---
title: Procesar resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21474aed83aac1fe86e2242b1238affa11ae64a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200317"
---
# <a name="process-results-odbc"></a>Procesar resultados (ODBC)
    
### <a name="to-process-results"></a>Para procesar resultados  
  
1.  Recupere información del conjunto de resultados.  
  
2.  Si se usan columnas enlazadas, por cada columna a la que quiera enlazar, llame a [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) para enlazar un búfer de programa a la columna.  
  
3.  Por cada fila del conjunto de resultados:  
  
    -   Llame a [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) para obtener la siguiente fila.  
  
    -   Si se utilizan columnas enlazadas, utilice los datos que están ahora disponibles en los búferes de columna enlazada.  
  
    -   Si se usan columnas sin enlazar, llame a [SQLGetData](../native-client-odbc-api/sqlgetdata.md) una o más veces para obtener los datos de las columnas sin enlazar después de la última columna enlazada. Las llamadas a `SQLGetData` deber estar en orden creciente de número de columna.  
  
    -   Llame a `SQLGetData` varias veces para obtener datos de una columna de texto o de imagen.  
  
4.  Cuando [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) señale el fin del conjunto de resultados devolviendo SQL_NO_DATA, llame a [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) para determinar si está disponible otro conjunto de resultados.  
  
    -   Si devuelve SQL_SUCCESS, está disponible otro conjunto de resultados.  
  
    -   Si devuelve SQL_NO_DATA, no hay ningún otro conjunto de resultados disponible.  
  
    -   Si devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR, llame a [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) para determinar si está disponible la salida de una instrucción PRINT o RAISERROR.  
  
         Si se utilizan parámetros de instrucción enlazados como parámetros de salida o como valor devuelto de un procedimiento almacenado, utilice los datos ahora disponibles en los búferes de parámetros enlazados. Asimismo, si se usan parámetros enlazados, cada llamada a [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) o [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) ejecutará la instrucción SQL *S* veces, donde *S* es el número de elementos en la matriz de parámetros enlazados. Esto significa que habrá *S* conjuntos de resultados para procesar, donde cada conjunto de resultados comprende todos los conjuntos de resultados, parámetros de salida y códigos de retorno devueltos normalmente por una ejecución única de la instrucción SQL.  
  
    > [!NOTE]  
    >  Cuando un conjunto de resultados contiene filas del cálculo, cada fila del cálculo está disponible como un conjunto de resultados independiente. Estos conjuntos de resultados de cálculo se intercalan entre las filas normales e interrumpen las filas normales en varios conjuntos de resultados.  
  
5.  Opcionalmente, llame a [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) con SQL_UNBIND para liberar los búferes de columna enlazada.  
  
6.  Si está disponible otro conjunto de resultados, vaya al paso 1.  
  
> [!NOTE]  
>  Para cancelar el procesamiento de un conjunto de resultados antes de que [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) devuelva SQL_NO_DATA, llame a [SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md).  
  
## <a name="see-also"></a>Vea también  
 [Temas de procedimientos de los resultados de procesamiento &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  
