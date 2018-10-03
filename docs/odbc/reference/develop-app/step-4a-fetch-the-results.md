---
title: 'Paso 4a: capturar los resultados | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cad33f1ccf798a08ef1f11667e59b4d5fb4888d8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730653"
---
# <a name="step-4a-fetch-the-results"></a>El paso 4a: capturar los resultados
El siguiente paso es recuperar los resultados, como se muestra en la siguiente ilustración.  
  
 ![Muestra cómo capturar resultados en una aplicación ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Si la instrucción ejecutada en "Paso 3: crear y ejecutar una instrucción SQL" fue una **seleccione** instrucción o una función de catálogo, la aplicación llama primero al **SQLNumResultCols** para determinar el número de columnas en el conjunto de resultados. Este paso no es necesario si la aplicación ya conoce el número del resultado de establecer las columnas, como cuando la instrucción SQL está codificado de forma rígida en una aplicación personalizada o vertical.  
  
 A continuación, la aplicación recupera el nombre, tipo de datos, precisión y escala de cada columna del conjunto de resultados con **SQLDescribeCol**. Nuevamente, esto no es necesario para las aplicaciones como aplicaciones verticales y personalizadas que ya conocen esta información. La aplicación pasa esta información para **SQLBindCol**, que enlaza una variable de aplicación con una columna del conjunto de resultados.  
  
 La aplicación llama **SQLFetch** para recuperar la primera fila de datos y colocar los datos de esa fila en las variables enlazadas con **SQLBindCol**. Si hay datos long en la fila, a continuación, llama a **SQLGetData** para recuperar los datos. La aplicación continúa llamar a **SQLFetch** y **SQLGetData** para recuperar los datos adicionales. Una vez finalizada la obtención de datos, llama a **SQLCloseCursor** para cerrar el cursor.  
  
 Para obtener una descripción completa de recuperación de resultados, vea [recuperar resultados (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md) y [recuperar resultados (avanzado)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 Ahora la aplicación devuelve al "Paso 3: crear y ejecutar una instrucción SQL" para ejecutar otra instrucción en la misma transacción; o continúa en "Paso 5: la transacción de confirmación" confirmar o revertir la transacción.
