---
title: Tamaño del conjunto de filas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fda38811fa876c9a0fad55e7f2ee7566ad3026d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67943762"
---
# <a name="rowset-size"></a>Tamaño del conjunto de filas
El tamaño del conjunto de filas que se va a usar depende de la aplicación. Normalmente, las aplicaciones basadas en pantalla siguen una de estas dos estrategias. La primera consiste en establecer el tamaño del conjunto de filas en el número de filas que se muestran en la pantalla. Si el usuario cambia el tamaño de la pantalla, la aplicación cambia el tamaño del conjunto de filas en consecuencia. La segunda consiste en establecer el tamaño del conjunto de filas en un número mayor, como 100, lo que reduce el número de llamadas al origen de datos. La aplicación se desplaza localmente en el conjunto de filas siempre que sea posible y captura nuevas filas solo cuando se desplaza fuera del conjunto de filas.  
  
 Otras aplicaciones, como los informes, tienden a establecer el tamaño del conjunto de filas en el mayor número de filas que la aplicación puede controlar razonablemente: con un conjunto de filas mayor, a veces se reduce la sobrecarga de red por fila. Exactamente lo grande que puede ser un conjunto de filas depende del tamaño de cada fila y de la cantidad de memoria disponible.  
  
 El tamaño del conjunto de filas se establece mediante una llamada a **SQLSetStmtAttr** con un argumento de *atributo* de SQL_ATTR_ROW_ARRAY_SIZE. La aplicación puede cambiar el tamaño del conjunto de filas, enlazar nuevos búferes de conjunto de filas (llamando a **SQLBindCol** o especificando un desplazamiento de enlace) incluso después de que se hayan capturado filas, o ambos. Las implicaciones de cambiar el tamaño del conjunto de filas dependen de la función:  
  
-   **SQLFetch** y **SQLFetchScroll** usan el tamaño del conjunto de filas en el momento de la llamada para determinar el número de filas que se van a capturar. Sin embargo, **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_NEXT incrementa el cursor basándose en el conjunto de filas de la captura anterior y, a continuación, captura un conjunto de filas basándose en el tamaño del conjunto de filas actual.  
  
-   **SQLSetPos** utiliza el tamaño del conjunto de filas que está en vigor en la llamada anterior a **SQLFetch** o **SQLFetchScroll**, porque **SQLSetPos** funciona en un conjunto de filas que ya se ha establecido. **SQLSetPos** también recogerá el nuevo tamaño del conjunto de filas si se ha llamado a **SQLBulkOperations** después de cambiar el tamaño del conjunto de filas.  
  
-   **SQLBulkOperations** usa el tamaño del conjunto de filas en vigor en el momento de la llamada, ya que realiza operaciones en una tabla independiente de cualquier conjunto de filas capturado.
