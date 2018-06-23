---
title: Procesar resultados (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fa20ed943be8195eb7719265d3bd2ef0aa26a38c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104466"
---
# <a name="process-results-odbc"></a>Procesar resultados (ODBC)
    
### <a name="to-process-results"></a>Para procesar resultados  
  
1.  Recupere información del conjunto de resultados.  
  
2.  Si se usan columnas enlazadas, por cada columna a la que quiera enlazar, llame a [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) para enlazar un búfer de programa a la columna.  
  
3.  Por cada fila del conjunto de resultados:  
  
    -   Llame a [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) para obtener la siguiente fila.  
  
    -   Si se utilizan columnas enlazadas, utilice los datos que están ahora disponibles en los búferes de columna enlazada.  
  
    -   Si se usan columnas sin enlazar, llame a [SQLGetData](../native-client-odbc-api/sqlgetdata.md) una o más veces para obtener los datos de las columnas sin enlazar después de la última columna enlazada. Las llamadas a `SQLGetData` deber estar en orden creciente de número de columna.  
  
    -   Llame a `SQLGetData` varias veces para obtener datos de una columna de texto o de imagen.  
  
4.  Cuando [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) señale el fin del conjunto de resultados devolviendo SQL_NO_DATA, llame a [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) para determinar si está disponible otro conjunto de resultados.  
  
    -   Si devuelve SQL_SUCCESS, está disponible otro conjunto de resultados.  
  
    -   Si devuelve SQL_NO_DATA, no hay ningún otro conjunto de resultados disponible.  
  
    -   Si devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR, llame a [SQLGetDiagRec](http://go.microsoft.com/fwlink/?LinkId=58402) para determinar si está disponible la salida de una instrucción PRINT o RAISERROR.  
  
         Si se utilizan parámetros de instrucción enlazados como parámetros de salida o como valor devuelto de un procedimiento almacenado, utilice los datos ahora disponibles en los búferes de parámetros enlazados. Asimismo, si se usan parámetros enlazados, cada llamada a [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) o [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) ejecutará la instrucción SQL *S* veces, donde *S* es el número de elementos en la matriz de parámetros enlazados. Esto significa que habrá *S* conjuntos de resultados para procesar, donde cada conjunto de resultados comprende todos los conjuntos de resultados, parámetros de salida y códigos de retorno devueltos normalmente por una ejecución única de la instrucción SQL.  
  
    > [!NOTE]  
    >  Cuando un conjunto de resultados contiene filas del cálculo, cada fila del cálculo está disponible como un conjunto de resultados independiente. Estos conjuntos de resultados de cálculo se intercalan entre las filas normales e interrumpen las filas normales en varios conjuntos de resultados.  
  
5.  Opcionalmente, llame a [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) con SQL_UNBIND para liberar los búferes de columna enlazada.  
  
6.  Si está disponible otro conjunto de resultados, vaya al paso 1.  
  
> [!NOTE]  
>  Para cancelar el procesamiento de un conjunto de resultados antes de que [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) devuelva SQL_NO_DATA, llame a [SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md).  
  
## <a name="see-also"></a>Vea también  
 [Temas "Cómo..." de resultados para procesar &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  