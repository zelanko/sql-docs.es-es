---
title: Cursores de bloques ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa35888ef93da9648fe6422bdc35ebf9da3a0525
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306356"
---
# <a name="block-cursors"></a>Cursores de bloque
Muchas aplicaciones pasan una cantidad significativa de tiempo trayendo datos a través de la red. Parte de este tiempo se dedica realmente a llevar los datos a través de la red, y parte de ellos se gasta en la sobrecarga de la red, como la llamada realizada por el controlador para solicitar una fila de datos. Este último tiempo se puede reducir si la aplicación hace un uso eficiente de *los cursores* de *bloque,* o *grasa,* que pueden devolver más de una fila a la vez.  
  
 Una aplicación siempre tiene la opción de utilizar un cursor de bloque. En los orígenes de datos desde los que solo se puede capturar una fila a la vez, los cursores de bloque deben simularse en el controlador. Esto se puede hacer mediante la realización de varias capturas de una sola fila. Aunque es poco probable que esto proporcione mejoras de rendimiento, abre oportunidades para las aplicaciones. Estas aplicaciones experimentarán aumentos de rendimiento a medida que los DBMS implementan cursores de bloque de forma nativa y los controladores asociados con esos DBMS los exponen.  
  
 Las filas devueltas en una sola captura con un cursor de bloque se denominan conjunto de *filas.* Es importante no confundir el conjunto de filas con el conjunto de resultados. El conjunto de resultados se mantiene en el origen de datos, mientras que el conjunto de filas se mantiene en los búferes de aplicación. Mientras el conjunto de resultados es fijo, el conjunto de filas no lo es: cambia la posición y el contenido cada vez que se captura un nuevo conjunto de filas. Del mismo modo que un cursor de una sola fila, como el cursor de solo avance de SQL tradicional, apunta a una fila actual, un cursor de bloque apunta al conjunto de filas, que se puede considerar como *filas actuales.*  
  
 Para realizar operaciones que funcionan en una sola fila cuando se han capturado varias filas, la aplicación debe indicar primero qué fila es la fila actual. Las llamadas a **SQLGetData** y las instrucciones de actualización y eliminación posicionadas requieren la fila actual. Cuando un cursor de bloque devuelve por primera vez un conjunto de filas, la fila actual es la primera fila del conjunto de filas. Para cambiar la fila actual, la aplicación llama a **SQLSetPos** o **SQLBulkOperations** (para actualizar por marcador). En la ilustración siguiente se muestra la relación del conjunto de resultados, el conjunto de filas, la fila actual, el cursor del conjunto de filas y el cursor de bloque. Para obtener más información, vea Uso de [cursores](../../../odbc/reference/develop-app/using-block-cursors.md)de bloque , más adelante en esta sección, y Instrucciones de [actualización y eliminación posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) y [Actualización de datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Captura de los conjuntos de filas siguiente, anterior, primero y último](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Si un cursor es un cursor de bloque es independiente de si es desplazable. Por ejemplo, la mayor parte del trabajo en una aplicación de informe se dedica a recuperar e imprimir filas. Debido a esto, funcionará más rápido con un cursor de bloque de solo avance. Utiliza un cursor de solo avance para evitar el gasto de un cursor desplazable y un cursor de bloque para reducir el tráfico de red.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Enlazar columnas para su uso con cursores de bloque](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Usar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matriz de Estados de fila](../../../odbc/reference/develop-app/row-status-array.md)
