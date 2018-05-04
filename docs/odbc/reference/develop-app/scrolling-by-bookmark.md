---
title: Desplazamiento por marcador | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 823929a98b3fc7b016f8bc1dc3fa1c2ed982b9c0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="scrolling-by-bookmark"></a>Desplazamiento por marcador
Al capturar filas con **SQLFetchScroll**, una aplicación puede utilizar un marcador como base para la selección de la fila inicial. Ésta es una forma de dirección absoluta porque no depende de la posición actual del cursor. Para desplazarse a una fila marcada, la aplicación llama **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK. Esta operación utiliza el marcador que señala el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR. Devuelve el conjunto de filas que comienza con la fila identificada por este marcador. Una aplicación puede especificar un desplazamiento para esta operación en el *FetchOffset* argumento de la llamada a **SQLFetchScroll**. Cuando se especifica un desplazamiento, la primera fila del conjunto de filas devuelto se determina sumando el número en el *FetchOffset* argumento según el número de la fila identificada por el marcador. Este uso de la *FetchOffset* no se admite cuando se usa con ODBC 2. *x* controladores; cuando una aplicación llama **SQLFetchScroll** en una API ODBC 2. *x* controlador con *FetchOrientation* establecido en SQL_FETCH_BOOKMARK, el *FetchOffset* argumento debe establecerse en 0.
