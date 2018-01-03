---
title: 'El paso 4a: capturar los resultados | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e799fb8290a2ea41093b0b4dcf2234cfc1d51a7e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="step-4a-fetch-the-results"></a>El paso 4a: capturar los resultados
El paso siguiente es capturar los resultados, como se muestra en la siguiente ilustración.  
  
 ![Muestra cómo capturar resultados en una aplicación ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Si la instrucción ejecutada en "Paso 3: crear y ejecutar una instrucción SQL" fue una **seleccione** instrucción o una función de catálogo, la aplicación llama primero **SQLNumResultCols** para determinar el número de columnas en el conjunto de resultados. Este paso no es necesario si la aplicación ya conoce el número del resultado de establecer las columnas, como cuando la instrucción SQL está codificado de forma rígida en una aplicación personalizada o vertical.  
  
 A continuación, la aplicación recupera el nombre, el tipo de datos, la precisión y la escala de cada columna del conjunto de resultados con **SQLDescribeCol**. Una vez más, esto no es necesario para las aplicaciones como aplicaciones verticales y personalizadas que ya conocen esta información. La aplicación pasa esta información a **SQLBindCol**, que enlaza una variable de aplicación con una columna del conjunto de resultados.  
  
 La aplicación llama **SQLFetch** para recuperar la primera fila de datos y colocar los datos de esa fila en las variables enlazadas con **SQLBindCol**. Si hay datos largos en la fila, a continuación, llama **SQLGetData** para recuperar los datos. La aplicación continúa llamar a **SQLFetch** y **SQLGetData** para recuperar datos adicionales. Cuando haya finalizado la obtención de datos, llama a **SQLCloseCursor** para cerrar el cursor.  
  
 Para obtener una descripción completa de la recuperación de resultados, vea [recuperar resultados (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md) y [recuperar resultados (avanzado)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 Ahora la aplicación vuelve al "Paso 3: crear y ejecutar una instrucción SQL" para ejecutar otra instrucción en la misma transacción; o continúa en "Paso 5: la transacción de confirmación" confirmar o revertir la transacción.
