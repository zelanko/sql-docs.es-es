---
title: Recuperación de resultados (avanzado) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca02b4ff911c8edff06b38d5341eeaa288cc194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294645"
---
# <a name="retrieving-results-advanced"></a>Al recuperar los resultados (avanzados)
Una aplicación puede especificar que se agregue un desplazamiento a las direcciones de búfer de datos enlazados y a las direcciones de búfer de longitud/indicador correspondientes cuando se llama a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos** . Los resultados de estas adiciones determinan las direcciones utilizadas en estas operaciones.  
  
 Los desplazamientos de enlace permiten a una aplicación cambiar los enlaces sin llamar a **SQLBindCol** para las columnas enlazadas anteriormente. Una llamada a **SQLBindCol** para volver a enlazar datos cambia la dirección del búfer y el puntero de longitud/indicador. Por otro lado, el reenlace con un desplazamiento simplemente agrega un desplazamiento a la dirección de búfer de datos enlazada existente y a la dirección del búfer de longitud/indicador. Cuando se utilizan desplazamientos, los enlaces son una "plantilla" de cómo se distribuyen los búferes de aplicación y la aplicación puede mover esta "plantilla" a diferentes áreas de memoria cambiando el desplazamiento. Se puede especificar un nuevo desplazamiento en cualquier momento y siempre se agrega a los valores enlazados originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR en la dirección de un búfer SQLINTEGER. Antes de que la aplicación llame a una función que usa los enlaces, como **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**, coloca un desplazamiento en bytes en este búfer, siempre que ni la dirección del búfer de datos ni la dirección del búfer de longitud/indicador sea 0 y siempre que la columna enlazada esté en el conjunto de resultados. La suma de la dirección y el desplazamiento debe ser una dirección válida. (Esto significa que el desplazamiento o ambos y la dirección a la que se agrega el desplazamiento pueden ser inválidos, siempre y cuando su suma sea una dirección válida.) El atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR es un puntero para que el valor de desplazamiento se pueda aplicar a más de un conjunto de datos de enlace, todos los cuales se pueden cambiar cambiando un valor de desplazamiento. Una aplicación debe asegurarse de que el puntero sigue siendo válido hasta que se cierra el cursor.  
  
> [!NOTE]  
>  ODBC 2 no admite los desplazamientos de enlace. *x* controladores.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [La biblioteca de cursores ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md)
