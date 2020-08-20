---
description: Usar cursores de bloque
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67cad7220641e9c3800e89675825cf2c0b1e334d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482868"
---
# <a name="using-block-cursors"></a>Usar cursores de bloque
La compatibilidad con los cursores de bloque está integrada en ODBC 3. *x*. **SQLFetch** solo se puede usar para las capturas de varias filas cuando se llama en ODBC 3. *x*; Si ODBC 2. la aplicación *x* llama a **SQLFetch**, solo abrirá un cursor de una sola fila y de solo avance. Cuando se trata de un ODBC 3. la aplicación *x* llama a **SQLFetch** en ODBC 2. *x* , devuelve una sola fila a menos que el controlador admita **SQLExtendedFetch**. Para obtener más información, vea [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) en el Apéndice G: instrucciones de controlador para la compatibilidad con versiones anteriores.  
  
 Para usar cursores de bloque, la aplicación establece el tamaño del conjunto de filas, enlaza los búferes del conjunto de filas (como se describe en la sección anterior), establece opcionalmente los atributos de instrucción SQL_ATTR_ROWS_FETCHED_PTR y SQL_ATTR_ROW_STATUS_PTR, y llama a **SQLFetch** o **SQLFetchScroll** para capturar un bloque de filas. La aplicación puede cambiar el tamaño del conjunto de filas y enlazar nuevos búferes de conjunto de filas (llamando a **SQLBindCol** o especificando un desplazamiento de enlace) incluso después de que se hayan capturado las filas.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tamaño del conjunto de filas](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Número de filas recuperadas y estado](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData y cursores de bloque; bloquear curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
