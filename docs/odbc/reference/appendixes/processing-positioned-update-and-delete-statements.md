---
title: Procesamiento sitúa instrucciones Update y Delete | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41b4fe248f815e63c48a8da70edc88a1cc173667
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028429"
---
# <a name="processing-positioned-update-and-delete-statements"></a>Procesamiento de instrucciones posicionadas Update y Delete
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Admite el cursor de biblioteca que coloca instrucciones update y delete reemplazando el **WHERE CURRENT OF** cláusula en dichas instrucciones con un **donde** cláusula que enumera los valores almacenados en su memoria caché para cada columna enlazada. La biblioteca de cursores pasa recién construido **actualización** y **eliminar** instrucciones para el controlador para la ejecución. Las instrucciones de actualización posicionada, la biblioteca de cursores, a continuación, actualiza su caché de los valores de los búferes de conjunto de filas y establece el valor correspondiente en la matriz de Estados de fila a SQL_ROW_UPDATED. Para instrucciones delete posicionadas, Establece el valor correspondiente en la matriz de Estados de fila a SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  El **donde** cláusula construido por la biblioteca de cursores para identificar la fila actual no puede identificar las filas, identificar una fila diferente o más de una fila. Para obtener más información, consulte [construir busca instrucciones](../../../odbc/reference/appendixes/constructing-searched-statements.md), más adelante en este apéndice.  
  
 Posicionadas update y delete las instrucciones son las siguientes restricciones:  
  
-   Posicionadas update y delete instrucciones se pueden usar sólo en los siguientes casos: cuando un **seleccione** instrucción puede generar el conjunto de resultados; cuando el **seleccione** instrucción no contenía una combinación, un  **Unión** cláusula, o un **GROUP BY** cláusula; y cuando las columnas que usan un alias o una expresión en la lista de selección no se enlazaron con **SQLBindCol**.  
  
-   Si una aplicación prepara una instrucción de eliminación o actualización posicionada, debe hacerlo después de haber llamado **SQLFetch** o **SQLFetchScroll**. Aunque la biblioteca de cursores envía la instrucción del controlador para la preparación, la instrucción se cierra y se ejecuta directamente cuando la aplicación llama **SQLExecute**.  
  
-   Si el controlador admite solo una instrucción activa, las capturas de biblioteca de cursor el resto del resultado establece y, a continuación, vuelve a obtener el conjunto de filas actual de su memoria caché antes de ejecutar una posición instrucción update o delete. Si la aplicación, a continuación, llama a una función que devuelve los metadatos en un conjunto de resultados (por ejemplo, **SQLNumResultCols** o **SQLDescribeCol**), la biblioteca de cursores devuelve un error.  
  
-   Si se realiza una actualización por posición o la instrucción delete en una columna de una tabla que incluye una columna de marca de tiempo que se actualiza automáticamente cada vez que se realiza una actualización, actualización posicionada posterior o las instrucciones delete se producirá un error si la columna de marca de tiempo enlazado. Esto ocurre porque la búsqueda de actualización o eliminación de instrucción que crea la biblioteca de cursores no identificará con precisión la fila para actualizar. El valor de la instrucción de búsqueda para la columna de marca de tiempo no coincidirá con el valor actualizado automáticamente de la columna de marca de tiempo.
