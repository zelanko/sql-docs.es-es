---
title: 'Paso 4a: Obtener los resultados de la página de resultados de la página de resultados de la página de resultados de la página de Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c4f810e5c42b54ec871c233ab498936abae610dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302976"
---
# <a name="step-4a-fetch-the-results"></a>Paso 4a: Captura de los resultados
El siguiente paso es capturar los resultados, como se muestra en la siguiente ilustración.  
  
 ![Muestra cómo capturar resultados en una aplicación ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Si la instrucción ejecutada en "Paso 3: Compilar y ejecutar una instrucción SQL" era una instrucción **SELECT** o una función de catálogo, la aplicación llama primero a **SQLNumResultCols** para determinar el número de columnas del conjunto de resultados. Este paso no es necesario si la aplicación ya conoce el número de columnas del conjunto de resultados, como cuando la instrucción SQL está codificada de forma rígida en una aplicación vertical o personalizada.  
  
 A continuación, la aplicación recupera el nombre, el tipo de datos, la precisión y la escala de cada columna de conjunto de resultados con **SQLDescribeCol**. Una vez más, esto no es necesario para aplicaciones como verticales y personalizadas que ya conocen esta información. La aplicación pasa esta información a **SQLBindCol**, que enlaza una variable de aplicación a una columna del conjunto de resultados.  
  
 La aplicación ahora llama a **SQLFetch** para recuperar la primera fila de datos y colocar los datos de esa fila en las variables enlazadas con **SQLBindCol**. Si hay datos largos en la fila, llama a **SQLGetData** para recuperar esos datos. La aplicación sigue llamando a **SQLFetch** y **SQLGetData** para recuperar datos adicionales. Una vez que ha terminado de capturar datos, llama a **SQLCloseCursor** para cerrar el cursor.  
  
 Para obtener una descripción completa de la recuperación de resultados, vea Recuperación de [resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md) y Recuperación de [resultados (avanzado)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 La aplicación ahora vuelve a "Paso 3: Compilar y ejecutar una instrucción SQL" para ejecutar otra instrucción en la misma transacción; o procede al "Paso 5: Confirmar la transacción" para confirmar o revertir la transacción.
