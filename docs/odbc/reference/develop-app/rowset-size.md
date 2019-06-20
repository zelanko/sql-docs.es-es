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
manager: craigg
ms.openlocfilehash: 54da54a63fb1234478a3161cd46e7143258d2d65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468682"
---
# <a name="rowset-size"></a>Tamaño del conjunto de filas
Qué tamaño del conjunto de filas que se usará depende de la aplicación. Normalmente, las aplicaciones basadas en la pantalla siguen uno de dos estrategias. La primera consiste en establecer el tamaño del conjunto de filas en el número de filas que se muestran en la pantalla; Si el usuario cambia el tamaño de la pantalla, la aplicación cambia el tamaño del conjunto de filas según corresponda. El segundo es establecer el tamaño del conjunto de filas en un número mayor, como 100, lo que reduce el número de llamadas al origen de datos. La aplicación se desplaza localmente en el conjunto de filas cuando sea posible y recupera nuevas filas solo cuando desplaza fuera del conjunto de filas.  
  
 Otras aplicaciones, como informes, tienden a establecer el tamaño del conjunto de filas para el mayor número de filas de la aplicación puede controlar razonablemente - con un conjunto de filas más grande, a veces se reduce la red sobrecarga por fila. Exactamente cómo de grande un conjunto de filas puede ser depende del tamaño de cada fila y la cantidad de memoria disponible.  
  
 Tamaño del conjunto de filas se establece mediante una llamada a **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. La aplicación puede cambiar el tamaño del conjunto de filas, enlazar nuevos búferes de conjunto de filas (mediante una llamada a **SQLBindCol** o especificando un desplazamiento de enlace) incluso después de que las filas se han capturado, o ambos. Las implicaciones de cambiar el tamaño del conjunto de filas dependen de la función:  
  
-   **SQLFetch** y **SQLFetchScroll** usar el tamaño del conjunto de filas en el momento de la llamada para determinar cuántas filas para capturar. Sin embargo, **SQLFetchScroll** con un *FetchOrientation* de incrementos SQL_FETCH_NEXT el cursor basado en el conjunto de filas de la captura anterior y, a continuación, capturas de un conjunto de filas en función del tamaño del conjunto de filas actual.  
  
-   **SQLSetPos** utiliza el tamaño del conjunto de filas que está en vigor a partir de la llamada anterior a **SQLFetch** o **SQLFetchScroll**, porque **SQLSetPos** opera en un conjunto de filas ya que se ha establecido. **SQLSetPos** también recogerá el nuevo tamaño del conjunto de filas si **SQLBulkOperations** se ha llamado después de que se cambió el tamaño del conjunto de filas.  
  
-   **SQLBulkOperations** utiliza el tamaño del conjunto de filas en vigor en el momento de la llamada, ya que realiza operaciones en una tabla independiente de cualquier conjunto de filas capturada.
