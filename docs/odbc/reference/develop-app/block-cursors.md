---
title: Los cursores de bloque | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: dc62e7b5225c434bac33630f2f0cf8f39c72bfc9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199291"
---
# <a name="block-cursors"></a>Cursores de bloque
Muchas aplicaciones dedican una cantidad considerable de tiempo que lleva los datos a través de la red. Parte de este tiempo se dedica a traer realmente los datos a través de la red, y parte de él se dedica a red sobrecarga, por ejemplo, la llamada realizada por el controlador para solicitar una fila de datos. Puede reducir el tiempo último si la aplicación realiza un uso eficaz de *bloque,* o *fat,* *cursores,* que puede devolver más de una fila a la vez.  
  
 Una aplicación siempre tiene la opción de usar un cursor de bloque. En los orígenes de datos desde el que se puede recuperar una única fila a la vez, se deben simular cursores de bloque en el controlador. Esto puede hacerse mediante la realización de varias recopilaciones de fila única. Aunque es poco probable que proporcione cualquier ganancia de rendimiento, abre oportunidades para las aplicaciones. Tales aplicaciones, a continuación, experimentará un aumento del rendimiento como DBMS implementan cursores de bloque de forma nativa y exponen los controladores asociados con los DBMS.  
  
 Las filas devueltas en una única captura con un cursor de bloque se denominan el *conjunto de filas*. Es importante no confundir el conjunto de filas con el conjunto de resultados. El conjunto de resultados se mantiene en el origen de datos, mientras se mantiene el conjunto de filas en búferes de la aplicación. Mientras el conjunto de resultados es fijo, el conjunto de filas no es: cambia la posición y el contenido de cada vez que se captura un nuevo conjunto de filas. Al igual que un cursor de fila única, como los puntos de cursor de solo avance SQL tradicionales a una fila actual, un cursor de bloque señala al conjunto de filas, que puede considerarse como *filas actuales*.  
  
 Para realizar operaciones que operan en una sola fila cuando se han capturado varias filas, la aplicación en primer lugar debe indicar qué fila es la fila actual. Se requiere la fila actual mediante llamadas a **SQLGetData** y actualización por posición y elimine las instrucciones. Cuando un cursor de bloque en primer lugar devuelve un conjunto de filas, la fila actual es la primera fila del conjunto de filas. Para cambiar la fila actual, la aplicación llama a **SQLSetPos** o **SQLBulkOperations** (para actualizar por marcador). La siguiente ilustración muestra la relación del conjunto de resultados, conjunto de filas, la fila actual, el cursor de conjunto de filas y cursor de bloque. Para obtener más información, consulte [utilizar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md), más adelante en esta sección, y [coloca actualizar y eliminar instrucciones](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) y [actualizar los datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![A continuación, capturar antes, primero y último conjuntos de filas](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Si un cursor es un cursor de bloque son independiente de si es desplazable. Por ejemplo, la mayoría del trabajo en una aplicación de informes se dedica a recuperar e imprimir las filas. Por este motivo, le trabajar más rápido con solo avance, cursor de bloque. Utiliza un cursor de solo avance para evitar el gasto de un cursor desplazable y un cursor de bloque para reducir el tráfico de red.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Enlazar columnas para su uso con cursores de bloque](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Usar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matriz de Estados de fila](../../../odbc/reference/develop-app/row-status-array.md)
