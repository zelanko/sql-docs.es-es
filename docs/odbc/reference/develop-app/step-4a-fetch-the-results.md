---
description: 'Paso 4a: Captura de los resultados'
title: 'Paso 4A: capturar los resultados | Microsoft Docs'
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
ms.openlocfilehash: 91a81809d07faafac6511bb5ec96c97d4f59d654
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491362"
---
# <a name="step-4a-fetch-the-results"></a>Paso 4a: Captura de los resultados
El siguiente paso consiste en capturar los resultados, tal como se muestra en la siguiente ilustración.  
  
 ![Muestra cómo capturar resultados en una aplicación ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Si la instrucción ejecutada en "paso 3: compilar y ejecutar una instrucción SQL" fuera una instrucción **Select** o una función de catálogo, la aplicación llama primero a **SQLNumResultCols** para determinar el número de columnas del conjunto de resultados. Este paso no es necesario si la aplicación ya conoce el número de columnas del conjunto de resultados, como cuando la instrucción SQL está codificada de forma rígida en una aplicación vertical o personalizada.  
  
 A continuación, la aplicación recupera el nombre, el tipo de datos, la precisión y la escala de cada columna del conjunto de resultados con **SQLDescribeCol**. De nuevo, esto no es necesario para aplicaciones como las aplicaciones verticales y personalizadas que ya conocen esta información. La aplicación pasa esta información a **SQLBindCol**, que enlaza una variable de aplicación a una columna en el conjunto de resultados.  
  
 Ahora la aplicación llama a **SQLFetch** para recuperar la primera fila de datos y colocar los datos de esa fila en las variables enlazadas con **SQLBindCol**. Si hay datos de gran tamaño en la fila, llama a **SQLGetData** para recuperar los datos. La aplicación continúa llamando a **SQLFetch** y **SQLGetData** para recuperar datos adicionales. Una vez finalizada la captura de datos, llama a **SQLCloseCursor** para cerrar el cursor.  
  
 Para obtener una descripción completa de cómo recuperar los resultados, vea [recuperar resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md) y [recuperar resultados (avanzado)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 La aplicación ahora vuelve al "paso 3: compilar y ejecutar una instrucción SQL" para ejecutar otra instrucción en la misma transacción; o bien, continúe con "paso 5: confirmar la transacción" para confirmar o revertir la transacción.
