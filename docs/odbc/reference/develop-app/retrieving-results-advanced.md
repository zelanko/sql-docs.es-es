---
title: Al recuperar los resultados (avanzados) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85ee85c9bb44f32d33cee622c60c677f22b0ba7c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-results-advanced"></a>Al recuperar los resultados (avanzados)
Una aplicación puede especificar que se ha agregado un desplazamiento a direcciones de búfer de datos y la longitud/indicador correspondiente enlazados búfer direcciones cuando **SQLBulkOperations**, **SQLFetch**, ** SQLFetchScroll**, o **SQLSetPos** se llama. Los resultados de estas adiciones determinarán las direcciones usadas en estas operaciones.  
  
 Desplazamientos de enlace permiten que una aplicación cambiar los enlaces sin llamar a **SQLBindCol** para las columnas enlazadas previamente. Una llamada a **SQLBindCol** volver a enlazar los datos cambia la dirección del búfer y el puntero de longitud/indicador. Volver a enlazar con un desplazamiento, por otro lado, simplemente agrega un desplazamiento a la dirección de búfer de datos enlazados existente y la dirección del búfer de longitud/indicador. Cuando se utilizan los desplazamientos, los enlaces son "plantilla" de cómo se distribuyen los búferes de la aplicación y la aplicación puede mover esta "plantilla" a diferentes áreas de memoria cambiando el desplazamiento. Un desplazamiento nuevo puede especificarse en cualquier momento y siempre se agrega a los valores enlazados originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción de SQL_ATTR_ROW_BIND_OFFSET_PTR a la dirección de un búfer SQLINTEGER. Antes de que la aplicación llama a una función que utiliza los enlaces, como **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**, que coloca un desplazamiento en bytes de este búfer, como la dirección del búfer de datos ni la dirección de búfer de longitud/indicador es 0, y siempre que la columna dependiente está en el conjunto de resultados. La suma de la dirección y el desplazamiento debe ser una dirección válida. (Esto significa que uno o ambos el desplazamiento y la dirección a la que se agrega el desplazamiento pueden ser válidos, como la suma es una dirección válida.) El atributo de instrucción de SQL_ATTR_ROW_BIND_OFFSET_PTR es un puntero para que el valor de desplazamiento se pueda aplicar a más de un conjunto de enlace de datos, que se puede cambiar si cambia un valor de desplazamiento. Una aplicación debe asegurarse de que el puntero es válido hasta que se cierra el cursor.  
  
> [!NOTE]  
>  Desplazamientos de enlace no son compatibles con ODBC 2. *x* controladores.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [La biblioteca de cursores ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Varios resultados](../../../odbc/reference/develop-app/multiple-results.md)

