---
title: Desplazamiento y captura filas (ODBC) | Documentos de Microsoft
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
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 273046a04849b0b1501e2dd4be476c9abb540c5f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Desplazamiento y captura filas (ODBC)
Cuando se utiliza un cursor desplazable, las aplicaciones llaman a **SQLFetchScroll** para colocar las filas del cursor y fetch. **SQLFetchScroll** permite el desplazamiento relativo (siguiente, anterior y relative *n* filas), desplazamiento absoluto (, apellidos y fila *n*) y el posicionamiento por marcador. El *FetchOrientation* y *FetchOffset* argumentos en **SQLFetchScroll** especificar qué filas que se va a capturar, como se muestra en los diagramas siguientes.  
  
 ![A continuación, capturar anterior, primero y último conjuntos de filas](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **A continuación, capturar conjuntos de filas de anterior, primero y último**  
  
 ![Capturar conjunto de filas absoluto, relativo y marcado](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Capturar conjuntos de filas absoluto, relativo y marcado**  
  
 **SQLFetchScroll** coloca el cursor a la fila especificada y devuelve las filas del conjunto de filas a partir de esa fila. Si el conjunto de filas especificado se solapa con el final del conjunto de resultados, se devuelve un conjunto de filas parcial. Establece si el conjunto de filas especificado se solapa con el inicio del resultado, el primer conjunto de filas en el resultado suele devolver conjunto; Para obtener información detallada, vea el [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) descripción de la función.  
  
 En algunos casos, la aplicación podría desear colocar el cursor sin tener que recuperar los datos. Por ejemplo, conviene comprobar si existe una fila u obtener solo el marcador de la fila sin volver a poner otros datos a través de la red. Para ello, Establece el atributo de instrucción de SQL_ATTR_RETRIEVE_DATA en SQL_RD_OFF. La variable enlazada a la columna de marcador (si existe) se actualiza siempre, independientemente de la configuración de este atributo de instrucción.  
  
 Después de recuperar el conjunto de filas, la aplicación puede llamar a **SQLSetPos** para situarse en una fila determinada en las filas del conjunto de filas o la actualización del conjunto de filas. Para obtener más información sobre el uso de **SQLSetPos**, consulte [actualizar los datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  Se admite el desplazamiento en 2 de ODBC. *x* controladores por **SQLExtendedFetch**. Para obtener más información, consulte [compatibilidad con versiones anteriores, los cursores desplazables y cursores de bloque](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.
