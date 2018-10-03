---
title: Desplazamiento y captura filas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 884c798e14964fbcaaf3ca9ba6656f4d62738fe8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642753"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Desplazamiento y captura filas (ODBC)
Cuando se usa un cursor desplazable, las aplicaciones llaman a **SQLFetchScroll** para colocar las filas del cursor y fetch. **SQLFetchScroll** admite el desplazamiento relativo (siguiente, anterior y relative *n* filas), desplazamiento absoluto (, apellidos y de fila *n*) y el posicionamiento por marcador. El *FetchOrientation* y *FetchOffset* argumentos en **SQLFetchScroll** especificar qué conjunto de filas para capturar, como se muestra en los diagramas siguientes.  
  
 ![A continuación, capturar antes, primero y último conjuntos de filas](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **A continuación, capturar conjuntos de filas anterior, primero y último**  
  
 ![Capturar conjunto de filas absoluto, relativo y marcado](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Recuperar conjuntos de filas absoluto, relativo y marcado**  
  
 **SQLFetchScroll** coloca el cursor a la fila especificada y devuelve las filas del conjunto de filas a partir de esa fila. Si el conjunto de filas especificado superpone al final del conjunto de resultados, se devuelve un conjunto de filas parcial. Establece si el conjunto de filas especificado se superpone con el inicio del resultado, el primer conjunto de filas en el resultado suele devolver conjunto; Para obtener información detallada, consulte el [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) descripción de la función.  
  
 En algunos casos, la aplicación podría colocar el cursor sin tener que recuperar todos los datos. Por ejemplo, podría comprobar si existe una fila o llevaba el marcador para la fila sin necesidad de otros datos a través de la red. Para ello, Establece el atributo de instrucción SQL_ATTR_RETRIEVE_DATA en SQL_RD_OFF. La variable enlazada a la columna de marcador (si existe) se actualiza siempre, independientemente de la configuración de este atributo de instrucción.  
  
 Después de recuperar el conjunto de filas, la aplicación puede llamar a **SQLSetPos** para situarse en una fila determinada en las filas del conjunto de filas o la actualización del conjunto de filas. Para obtener más información sobre el uso de **SQLSetPos**, consulte [actualizar los datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  El desplazamiento es compatible con ODBC 2. *x* controladores por **SQLExtendedFetch**. Para obtener más información, consulte [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)en Apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.
