---
title: "Tamaño del conjunto de filas | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e693a799c737baf8a11064c5bd50c2618cd1e29a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="rowset-size"></a>Tamaño del conjunto de filas
En función de qué tamaño de conjunto de filas que se usará en la aplicación. Normalmente, las aplicaciones basadas en pantalla siguen uno de dos estrategias. La primera consiste en establecer el tamaño del conjunto de filas en el número de filas que se muestran en la pantalla; Si el usuario cambia el tamaño de la pantalla, la aplicación también cambia el tamaño del conjunto de filas. La segunda es establecer el tamaño del conjunto de filas en un número mayor, como 100, lo que reduce el número de llamadas al origen de datos. La aplicación se desplaza localmente en el conjunto de filas siempre que sea posible y captura filas nuevas solo cuando desplaza fuera del conjunto de filas.  
  
 Otras aplicaciones, como informes, tienden a establecer el tamaño del conjunto de filas en el número máximo de filas que la aplicación puede controlar razonablemente, con un conjunto de filas más grande, a veces se reduce la red sobrecarga por fila. Exactamente lo grande un conjunto de filas puede ser depende del tamaño de cada fila y la cantidad de memoria disponible.  
  
 Tamaño de conjunto de filas se establece mediante una llamada a **SQLSetStmtAttr** con una *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. La aplicación puede cambiar el tamaño del conjunto de filas, enlazar nuevos búferes de conjunto de filas (mediante una llamada a **SQLBindCol** o especificando un desplazamiento de enlace) incluso después de que se han capturado filas, o ambos. Las implicaciones del cambio del tamaño del conjunto de filas dependen de la función:  
  
-   **SQLFetch** y **SQLFetchScroll** usar el tamaño del conjunto de filas en el momento de la llamada para determinar el número de filas para capturar. Sin embargo, **SQLFetchScroll** con un *FetchOrientation* de incrementos SQL_FETCH_NEXT el cursor basado en el conjunto de filas de la captura anterior y, a continuación, capturas un conjunto de filas en función del tamaño del conjunto de filas actual.  
  
-   **SQLSetPos** utiliza el tamaño de conjunto de filas que está en vigor a partir de la llamada anterior a **SQLFetch** o **SQLFetchScroll**, porque **SQLSetPos** funciona en un conjunto de filas que ya se ha establecido. **SQLSetPos** también recogerá el nuevo tamaño de conjunto de filas si **SQLBulkOperations** se ha llamado después de que se cambió el tamaño del conjunto de filas.  
  
-   **SQLBulkOperations** utiliza el tamaño de conjunto de filas en vigor en el momento de la llamada, ya que realiza operaciones en una tabla independiente de cualquier conjunto de filas capturada.
