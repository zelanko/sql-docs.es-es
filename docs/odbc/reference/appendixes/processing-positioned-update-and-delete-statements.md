---
title: Procesamiento coloca instrucciones Update y Delete | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 367062f5e671b366771b1a04f129b8e312f48cca
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="processing-positioned-update-and-delete-statements"></a>Procesamiento coloca instrucciones Update y Delete
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 El admite de biblioteca de cursor colocado instrucciones update y delete si se reemplaza el **WHERE CURRENT OF** cláusula en dichas instrucciones con un **donde** cláusula que enumera los valores almacenados en su caché para cada columna enlazada. La biblioteca de cursores pasa recién construido **actualización** y **eliminar** instrucciones para el controlador para la ejecución. Las instrucciones de actualización por posición, la biblioteca de cursores, a continuación, actualiza su caché de los valores de los búferes de conjunto de filas y establece el valor correspondiente en la matriz de Estados de fila a SQL_ROW_UPDATED. Para instrucciones delete posicionadas, Establece el valor correspondiente en la matriz de Estados de fila a SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  El **donde** cláusula construido por la biblioteca de cursores para identificar la fila actual no puede identificar las filas, identificar una fila diferente o más de una fila. Para obtener más información, consulte [construir instrucciones buscar](../../../odbc/reference/appendixes/constructing-searched-statements.md), más adelante en este apéndice.  
  
 Coloca update y delete instrucciones están sujetos a las restricciones siguientes:  
  
-   Coloca update y delete instrucciones se pueden usar sólo en los siguientes casos: cuando un **seleccione** instrucción genera el conjunto de resultados; si la **seleccione** instrucción no contenía una combinación, un  **Unión** cláusula, o un **GROUP BY** cláusula; y cuando no se enlazaron columnas que utilicen un alias o una expresión en la lista de selección con **SQLBindCol**.  
  
-   Si una aplicación prepara una actualización por posición o una instrucción delete, debe hacerlo después de haber llamado **SQLFetch** o **SQLFetchScroll**. Aunque la biblioteca de cursores envía la instrucción del controlador para la preparación, se cierra la instrucción y lo ejecuta directamente cuando la aplicación llama **SQLExecute**.  
  
-   Si el controlador admite solo una instrucción activa, las capturas de biblioteca de cursor el resto del resultado establece y, a continuación, vuelve a obtener el conjunto de filas actual desde la memoria caché antes de ejecutar una posición instrucción update o delete. Si la aplicación, a continuación, llama a una función que devuelve los metadatos en un conjunto de resultados (por ejemplo, **SQLNumResultCols** o **SQLDescribeCol**), la biblioteca de cursores devuelve un error.  
  
-   Si se realiza una actualización por posición o una instrucción delete en una columna de una tabla que incluye una columna de marca de tiempo que se actualiza automáticamente cada vez que se realiza una actualización, actualización posicionada posterior o las instrucciones delete se producirá un error si la columna de marca de tiempo enlazado. Esto ocurre porque la búsqueda se actualiza o elimina instrucción que crea la biblioteca de cursores no identificará con precisión la fila que se va a actualizar. El valor de la instrucción por búsqueda para la columna de marca de tiempo no coincidirá con el valor actualizado automáticamente de la columna de marca de tiempo.

