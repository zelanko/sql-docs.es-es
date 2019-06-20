---
title: Usar cursores de bloque | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 388995cd5cb8a711d72533685c14088a7e908475
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313506"
---
# <a name="using-block-cursors"></a>Usar cursores de bloque
Compatibilidad con cursores de bloque se integra en ODBC 3. *x*. **SQLFetch** puede usarse solo para las recuperaciones de varias filas cuando se llama en ODBC 3. *x*; si un ODBC 2. *x* aplicación llama a **SQLFetch**, abrirá un cursor sola fila y de solo avance. Cuando un ODBC 3. *x* aplicación llama a **SQLFetch** en un ODBC 2. *x* controlador, devuelve una sola fila a menos que el controlador admite **SQLExtendedFetch**. Para obtener más información, consulte [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
 Para utilizar cursores de bloque, la aplicación establece el tamaño del conjunto de filas, enlaza los búferes de conjunto de filas (como se describe en la sección anterior), opcionalmente, Establece los atributos de instrucción SQL_ATTR_ROWS_FETCHED_PTR y SQL_ATTR_ROW_STATUS_PTR y llamadas **SQLFetch**  o **SQLFetchScroll** para capturar un bloque de filas. La aplicación puede cambiar el tamaño del conjunto de filas y enlazar nuevos búferes de conjunto de filas (mediante una llamada a **SQLBindCol** o especificando un desplazamiento de bind) incluso después de que las filas se han capturado.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tamaño del conjunto de filas](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Número de filas recuperadas y estado](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData y cursores de bloque; curso de bloque](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
