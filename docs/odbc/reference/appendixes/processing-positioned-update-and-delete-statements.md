---
title: Procesamiento de las declaraciones de actualización y eliminación posicionadas de la sección de procesamiento de la sección de Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b3f20da018bcd4e28e8ffca097fb5a4373d7f42
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308026"
---
# <a name="processing-positioned-update-and-delete-statements"></a>Procesamiento de instrucciones posicionadas Update y Delete
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 La biblioteca de cursores admite instrucciones de actualización y eliminación posicionadas reemplazando la cláusula **WHERE CURRENT OF** en dichas instrucciones por una cláusula **WHERE** que enumera los valores almacenados en su caché para cada columna enlazada. La biblioteca de cursores pasa las instrucciones **UPDATE** y **DELETE** recién construidas al controlador para su ejecución. Para las instrucciones de actualización posicionadas, la biblioteca de cursores actualiza su caché a partir de los valores de los búferes del conjunto de filas y establece el valor correspondiente en la matriz de estado de fila en SQL_ROW_UPDATED. Para las instrucciones delete posicionadas, establece el valor correspondiente en la matriz de estado de fila en SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  La cláusula **WHERE** construida por la biblioteca de cursores para identificar la fila actual puede no identificar filas, identificar una fila diferente o identificar más de una fila. Para obtener más información, vea [Construir instrucciones buscadas](../../../odbc/reference/appendixes/constructing-searched-statements.md), más adelante en este apéndice.  
  
 Las instrucciones de actualización y eliminación posicionadas están sujetas a las siguientes restricciones:  
  
-   Las instrucciones update y delete posicionadas solo se pueden utilizar en los siguientes casos: cuando una instrucción **SELECT** generó el conjunto de resultados; cuando la instrucción **SELECT** no contenía una combinación, una cláusula **UNION** o una cláusula **GROUP BY;** y cuando las columnas que utilizaban un alias o expresión en la lista de selección no estaban enlazadas con **SQLBindCol**.  
  
-   Si una aplicación prepara una instrucción de actualización o eliminación posicionada, debe hacerlo después de haber llamado a **SQLFetch** o **SQLFetchScroll**. Aunque la biblioteca de cursores envía la instrucción al controlador para su preparación, cierra la instrucción y la ejecuta directamente cuando la aplicación llama a **SQLExecute**.  
  
-   Si el controlador solo admite una instrucción active, la biblioteca de cursores recupera el resto del conjunto de resultados y, a continuación, recupera el conjunto de filas actual de su caché antes de ejecutar una instrucción update o delete posicionada. Si la aplicación llama a una función que devuelve metadatos en un conjunto de resultados (por ejemplo, **SQLNumResultCols** o **SQLDescribeCol**), la biblioteca de cursores devuelve un error.  
  
-   Si se realiza una instrucción de actualización o eliminación posicionada en una columna de una tabla que incluye una columna de marca de tiempo que se actualiza automáticamente cada vez que se realiza una actualización, se producirá un error en todas las instrucciones de actualización o eliminación posicionadas posteriores si se enlaza la columna de marca de tiempo. Esto se produce porque la instrucción de actualización o eliminación buscada que crea la biblioteca de cursores no identificará con precisión la fila que se va a actualizar. El valor de la instrucción buscada para la columna timestamp no coincidirá con el valor actualizado automáticamente de la columna timestamp.
