---
title: Desplazamiento y obtención de filas (ODBC) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72d262bf73e69388f65ff281e62235d2d831669e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304206"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Desplazamiento y captura filas (ODBC)
Cuando se utiliza un cursor desplazable, las aplicaciones llaman a **SQLFetchScroll** para colocar el cursor y capturar filas. **SQLFetchScroll** admite el desplazamiento relativo (filas siguientes, anteriores y *relativas n),* el desplazamiento absoluto (primera, última y fila *n*) y la colocación por marcador. Los argumentos *FetchOrientation* y *FetchOffset* de **SQLFetchScroll** especifican qué conjunto de filas se va a capturar, como se muestra en los diagramas siguientes.  
  
 ![Captura de los conjuntos de filas siguiente, anterior, primero y último](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Captura de los conjuntos de filas siguiente, anterior, primero y último**  
  
 ![Captura del conjunto de filas absoluto, relativo y marcado](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Obtención de conjuntos de filas absolutos, relativos y marcados**  
  
 **SQLFetchScroll** coloca el cursor en la fila especificada y devuelve las filas del conjunto de filas a partir de esa fila. Si el conjunto de filas especificado se superpone al final del conjunto de resultados, se devuelve un conjunto de filas parcial. Si el conjunto de filas especificado se superpone al inicio del conjunto de resultados, normalmente se devuelve el primer conjunto de filas del conjunto de resultados; Para obtener detalles completos, consulte la descripción de la función [SQLFetchScroll.](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
 En algunos casos, es posible que la aplicación desee colocar el cursor sin recuperar ningún dato. Por ejemplo, es posible que desee probar si existe una fila o simplemente obtener el marcador de la fila sin traer otros datos a través de la red. Para ello, establece el atributo de instrucción SQL_ATTR_RETRIEVE_DATA en SQL_RD_OFF. La variable enlazada a la columna de marcador (si existe) siempre se actualiza, independientemente de la configuración de este atributo de instrucción.  
  
 Una vez recuperado el conjunto de filas, la aplicación puede llamar a **SQLSetPos** para colocarlo en una fila determinada del conjunto de filas o actualizar filas del conjunto de filas. Para obtener más información sobre el uso de **SQLSetPos**, vea [Actualización de datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  El desplazamiento se admite en ODBC 2. *x* controladores de **SQLExtendedFetch**. Para obtener más información, consulte Cursores de [bloque, cursores desplazables y Compatibilidad con versiones](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)anteriores en apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.
