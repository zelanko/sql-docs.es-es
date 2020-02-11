---
title: Desplazamiento y captura de filas (ODBC) | Microsoft Docs
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
ms.openlocfilehash: b326ed0c4e9a196904aa0f5c60b705243ef3bd97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061583"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Desplazamiento y captura filas (ODBC)
Cuando se usa un cursor desplazable, las aplicaciones llaman a **SQLFetchScroll** para colocar el cursor y capturar las filas. **SQLFetchScroll** admite el desplazamiento relativo (siguiente, anterior y relativo *n* filas), desplazamiento absoluto (primero, último y fila *n*) y posicionamiento por marcador. Los argumentos *FetchOrientation* y *FetchOffset* de **SQLFetchScroll** especifican qué conjunto de filas se va a capturar, tal como se muestra en los diagramas siguientes.  
  
 ![Captura de los conjuntos de filas siguiente, anterior, primero y último](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Captura de los conjuntos de filas siguiente, anterior, primero y último**  
  
 ![Captura del conjunto de filas absoluto, relativo y marcado](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Capturar conjuntos de filas absolutos, relativos y con marcadores**  
  
 **SQLFetchScroll** coloca el cursor en la fila especificada y devuelve las filas del conjunto de filas a partir de esa fila. Si el conjunto de filas especificado se superpone al final del conjunto de resultados, se devuelve un conjunto de filas parcial. Si el conjunto de filas especificado se superpone al inicio del conjunto de resultados, normalmente se devuelve el primer conjunto de filas del conjunto de resultados; para obtener detalles completos, vea la descripción de la función [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) .  
  
 En algunos casos, es posible que la aplicación desee colocar el cursor sin recuperar ningún dato. Por ejemplo, puede que desee probar si existe una fila o simplemente obtener el marcador de la fila sin traer otros datos a través de la red. Para ello, establece el atributo de instrucción SQL_ATTR_RETRIEVE_DATA en SQL_RD_OFF. La variable enlazada a la columna de marcador (si existe) siempre se actualiza, independientemente de la configuración de este atributo de instrucción.  
  
 Una vez recuperado el conjunto de filas, la aplicación puede llamar a **SQLSetPos** para colocarlo en una fila determinada del conjunto de filas o actualizar las filas del conjunto de filas. Para obtener más información sobre el uso de **SQLSetPos**, vea [actualizar datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  El desplazamiento se admite en ODBC 2. *x* controladores por **SQLExtendedFetch**. Para obtener más información, vea [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)en el Apéndice G: instrucciones de controlador para la compatibilidad con versiones anteriores.
