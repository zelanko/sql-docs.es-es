---
title: Al recuperar los resultados (avanzados) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020505"
---
# <a name="retrieving-results-advanced"></a>Al recuperar los resultados (avanzados)
Una aplicación puede especificar que se agrega un desplazamiento que va a enlazar las direcciones de búfer de datos y el indicador de longitud correspondiente direcciones de búfer cuando **SQLBulkOperations**, **SQLFetch**,  **SQLFetchScroll**, o **SQLSetPos** se llama. Los resultados de estas adiciones determinarán las direcciones usadas en estas operaciones.  
  
 Desplazamientos de enlace permite que una aplicación cambiar los enlaces sin llamar a **SQLBindCol** las columnas enlazadas anteriormente. Una llamada a **SQLBindCol** para volver a enlazar datos cambia la dirección del búfer y el puntero de longitud/indicador. Volver a enlazar con un desplazamiento, por otro lado, simplemente agrega un desplazamiento a la dirección de búfer de datos enlazados existente y la dirección del búfer de longitud/indicador. Cuando se utilizan los desplazamientos, los enlaces son una "plantilla" de la disposición de los búferes de la aplicación y la aplicación puede mover esta "plantilla" a diferentes áreas de memoria cambiando el desplazamiento. Un nuevo desplazamiento puede especificarse en cualquier momento y siempre se agrega a los valores enlazados originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR a la dirección de un búfer SQLINTEGER. Antes de la aplicación llama a una función que usa los enlaces, como **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**, coloca un desplazamiento en bytes de este búfer, siempre y cuando la dirección del búfer de datos ni la dirección del búfer de longitud/indicador es 0, y siempre y cuando la columna dependiente está en el conjunto de resultados. La suma de la dirección y el desplazamiento debe ser una dirección válida. (Esto significa que uno o ambos el desplazamiento y la dirección a la que se agrega el desplazamiento pueden ser válidos, siempre y cuando su suma es una dirección válida.) El atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR es un puntero para que el valor de desplazamiento se puede aplicar a más de un conjunto de enlace de datos, que se puede cambiar si cambia un valor de desplazamiento. Una aplicación debe asegurarse de que el puntero es válido hasta que se cierra el cursor.  
  
> [!NOTE]  
>  No se admiten los desplazamientos de enlace por ODBC 2. *x* controladores.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [La biblioteca de cursores ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md)
