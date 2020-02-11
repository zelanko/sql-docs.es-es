---
title: Cursores de bloque | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e0ea6ff655140c979f400f67a59cd7259bac9e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118819"
---
# <a name="block-cursors"></a>Cursores de bloque
Muchas aplicaciones invierten una cantidad considerable de tiempo en la incorporación de datos a través de la red. Parte de este tiempo se dedica a la realización real de los datos a través de la red y parte del mismo se dedica a la sobrecarga de la red, como la llamada realizada por el controlador para solicitar una fila de datos. Esta última vez se puede reducir si la aplicación hace un uso eficaz de los *cursores* de *bloque,* o *FAT,* que pueden devolver más de una fila a la vez.  
  
 Una aplicación siempre tiene la opción de usar un cursor de bloque. En los orígenes de datos de los que solo se puede capturar una fila cada vez, se deben simular cursores de bloque en el controlador. Esto puede realizarse mediante la realización de varias capturas de fila única. Aunque es improbable que esto ofrezca mejoras de rendimiento, se abren oportunidades para las aplicaciones. De este modo, las aplicaciones experimentarán un aumento del rendimiento, ya que los DBMS implementan los cursores de bloque de forma nativa y los controladores asociados a dichos DBMS los exponen.  
  
 Las filas devueltas en una captura única con un cursor de bloque se denominan *conjunto de filas*. Es importante no confundir el conjunto de filas con el conjunto de resultados. El conjunto de resultados se mantiene en el origen de datos, mientras que el conjunto de filas se mantiene en los búferes de la aplicación. Si bien el conjunto de resultados es fijo, no se cambia la posición y el contenido cada vez que se captura un nuevo conjunto de filas. Del mismo modo que un cursor de una sola fila, como el cursor de solo avance de SQL tradicional apunta a una fila actual, un cursor de bloque apunta al conjunto de filas, que se puede considerar como *filas actuales*.  
  
 Para realizar operaciones que operan en una sola fila cuando se han capturado varias filas, la aplicación debe indicar primero qué fila es la fila actual. La fila actual es necesaria para las llamadas **a las** instrucciones Update y posicionadas y DELETE. Cuando un cursor de bloque devuelve primero un conjunto de filas, la fila actual es la primera fila del conjunto de filas. Para cambiar la fila actual, la aplicación llama a **SQLSetPos** o **SQLBulkOperations** (para actualizar por marcador). En la ilustración siguiente se muestra la relación del conjunto de resultados, el conjunto de filas, la fila actual, el cursor de conjunto de filas y el cursor de bloque. Para obtener más información, vea [usar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md), más adelante en esta sección, y [instrucciones Update y DELETE posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) y [actualizar datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Captura de los conjuntos de filas siguiente, anterior, primero y último](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 El hecho de que un cursor sea un cursor de bloque es independiente de si es desplazable. Por ejemplo, la mayor parte del trabajo en una aplicación de informe se dedica a recuperar e imprimir filas. Por este motivo, funcionará más rápido con un cursor de bloque de solo avance. Utiliza un cursor de solo avance para evitar el gasto de un cursor desplazable y un cursor de bloqueo para reducir el tráfico de red.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Enlazar columnas para su uso con cursores de bloque](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Usar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matriz de Estados de fila](../../../odbc/reference/develop-app/row-status-array.md)
