---
title: Desplazarse por marcador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d27c46407e2994960af4f6abddd6cdc6f08ec852
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055539"
---
# <a name="scrolling-by-bookmark"></a>Desplazamiento por marcador
Al capturar filas con **SQLFetchScroll**, una aplicación puede usar un marcador como base para seleccionar la fila inicial. Ésta es una forma de dirección absoluta porque no depende de la posición actual del cursor. Para desplazarse a una fila marcada, la aplicación llama a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK. Esta operación usa el marcador al que apunta el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR. Devuelve el conjunto de filas que comienza con la fila identificada por este marcador. Una aplicación puede especificar un desplazamiento para esta operación en el argumento *FetchOffset* de la llamada a **SQLFetchScroll**. Cuando se especifica un desplazamiento, la primera fila del conjunto de filas devuelto se determina agregando el número del argumento *FetchOffset* al número de la fila identificada por el marcador. Este uso del argumento *FetchOffset* no se admite cuando se usa con ODBC 2. Controladores *x* ; Cuando una aplicación llama a **SQLFetchScroll** en ODBC 2. controlador *x* con *FetchOrientation* establecido en SQL_FETCH_BOOKMARK, el argumento *FetchOffset* debe establecerse en 0.
