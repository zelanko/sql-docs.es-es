---
title: Desplazamiento por marcador ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 454e29abdf848fdf4f4eaae090e7cc326f0048df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304196"
---
# <a name="scrolling-by-bookmark"></a>Desplazamiento por marcador
Al capturar filas con **SQLFetchScroll**, una aplicación puede usar un marcador como base para seleccionar la fila inicial. Ésta es una forma de dirección absoluta porque no depende de la posición actual del cursor. Para desplazarse a una fila marcada, la aplicación llama a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK. Esta operación utiliza el marcador al que apunta el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR. Devuelve el conjunto de filas que comienza con la fila identificada por este marcador. Una aplicación puede especificar un desplazamiento para esta operación en el *FetchOffset* argumento de la llamada a **SQLFetchScroll**. Cuando se especifica un desplazamiento, la primera fila del conjunto de filas devuelto se determina agregando el número del argumento *FetchOffset* al número de la fila identificada por el marcador. Este uso de la *FetchOffset* argumento no se admite cuando se utiliza con ODBC 2. *x* controladores; cuando una aplicación llama a **SQLFetchScroll** en un ODBC 2. *x* controlador con *FetchOrientation* establecido en SQL_FETCH_BOOKMARK, el *FetchOffset* argumento debe establecerse en 0.
