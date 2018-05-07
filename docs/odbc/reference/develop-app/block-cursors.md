---
title: Los cursores de bloque | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21bbfa223e2eb58df8fc89b69f7f9df3c08983e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="block-cursors"></a>Cursores de bloque
Muchas aplicaciones dedican una cantidad considerable de tiempo que lleva los datos a través de la red. Parte de este tiempo se invierte realmente volver a poner los datos a través de la red, y parte de ella se dedica a la sobrecarga, de la red, como la llamada realizada por el controlador para solicitar una fila de datos. Si la aplicación realiza un uso eficaz de la última vez que se puede reducir *bloque,* o *fat,* *cursores,* que puede devolver más de una fila a la vez.  
  
 Una aplicación siempre tiene la opción de usar un cursor de bloque. En los orígenes de datos desde el que se puede recuperar sólo una fila a la vez, se deben simular cursores de bloque en el controlador. Esto puede hacerse mediante la realización de varias recopilaciones de varias filas. Aunque es poco probable proporcionar las mejoras de rendimiento, se abre oportunidades para las aplicaciones. Estas aplicaciones, a continuación, experimentará un aumento del rendimiento como DBMS implementan cursores de bloque de forma nativa y los controladores asociados a esos DBMS exponen.  
  
 Las filas devueltas en una sola operación de obtención con un cursor de bloque se denominan el *conjunto de filas*. Es importante no confundir el conjunto de filas con el conjunto de resultados. El conjunto de resultados se mantiene en el origen de datos, mientras se mantiene el conjunto de filas en búferes de la aplicación. Mientras que el conjunto de resultados es fija, no es el conjunto de filas, cambia de posición y el contenido de cada vez que se captura un nuevo conjunto de filas. Al igual que un cursor de varias filas, como los puntos de cursor de solo avance tradicionales de SQL a una fila actual, un cursor de bloque señala al conjunto de filas, que puede considerarse como *filas actuales*.  
  
 Para realizar operaciones que operan en una sola fila cuando se han capturado varias filas, la aplicación debe indicar qué fila es la fila actual. Se requiere la fila actual mediante llamadas a **SQLGetData** y actualización por posición y elimine las instrucciones. Cuando un cursor de bloque en primer lugar devuelve un conjunto de filas, la fila actual es la primera fila del conjunto de filas. Para cambiar la fila actual, la aplicación llama **SQLSetPos** o **SQLBulkOperations** (para actualizar por marcador). En la siguiente ilustración muestra la relación del conjunto de resultados, conjunto de filas, fila actual, el cursor de conjunto de filas y cursor de bloque. Para obtener más información, consulte [utilizar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md), más adelante en esta sección, y [actualización coloca y eliminar instrucciones](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) y [actualizar los datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![A continuación, capturar anterior, primero y último conjuntos de filas](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Si un cursor es un cursor de bloque son independiente de si es desplazable. Por ejemplo, la mayoría del trabajo en una aplicación de informes se dedica recuperar e imprimir filas. Por este motivo, este se funcionan con más rapidez con solo avance, cursor de bloque. Utiliza un cursor de solo avance para evitar el gasto de un cursor desplazable y un cursor de bloque para reducir el tráfico de red.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Enlazar columnas para su uso con cursores de bloque](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Usar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matriz de Estados de fila](../../../odbc/reference/develop-app/row-status-array.md)
