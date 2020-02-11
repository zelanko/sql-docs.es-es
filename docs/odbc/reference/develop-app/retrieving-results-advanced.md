---
title: Recuperando resultados (avanzado) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22a88a96b856ba0976dcb8600d26f78b772654bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020505"
---
# <a name="retrieving-results-advanced"></a>Al recuperar los resultados (avanzados)
Una aplicación puede especificar que se agregue un desplazamiento a las direcciones de búfer de datos enlazadas y a las direcciones de búfer de indicador de longitud/indicador correspondientes cuando se llama a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos** . Los resultados de estas adiciones determinan las direcciones utilizadas en estas operaciones.  
  
 Los desplazamientos de enlace permiten a una aplicación cambiar los enlaces sin llamar a **SQLBindCol** para las columnas enlazadas previamente. Una llamada a **SQLBindCol** para volver a enlazar los datos cambia la dirección del búfer y el puntero de longitud/indicador. Al volver a enlazar con un desplazamiento, por otro lado, simplemente se agrega un desplazamiento a la dirección del búfer de datos enlazado existente y la dirección del búfer del indicador/longitud. Cuando se usan desplazamientos, los enlaces son una "plantilla" de cómo se colocan los búferes de la aplicación y la aplicación puede moverla a distintas áreas de memoria cambiando el desplazamiento. Se puede especificar un nuevo desplazamiento en cualquier momento y siempre se agrega a los valores enlazados originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR en la dirección de un búfer SQLINTEGER donde. Antes de que la aplicación llame a una función que usa los enlaces, como **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**, coloca un desplazamiento en bytes en este búfer, siempre y cuando la dirección del búfer de datos o la dirección del búfer de longitud/indicador sea 0, y siempre que la columna enlazada esté en el conjunto de resultados. La suma de la dirección y el desplazamiento debe ser una dirección válida. (Esto significa que el desplazamiento y la dirección a la que se agrega el desplazamiento pueden ser no válidos, siempre que su suma sea una dirección válida). El atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR es un puntero para que el valor de desplazamiento pueda aplicarse a más de un conjunto de datos de enlace; todos ellos se pueden cambiar cambiando un valor de desplazamiento. Una aplicación debe asegurarse de que el puntero siga siendo válido hasta que se cierre el cursor.  
  
> [!NOTE]  
>  Los desplazamientos de enlace no son compatibles con ODBC 2. Controladores *x* .  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [La biblioteca de cursores ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md)
