---
title: Cursores | Microsoft Docs
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
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 55a10004936cc2333eca14fd66123b929e8b9e5c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cursors"></a>Cursores
Una aplicación captura los datos con un *cursor*. Un cursor es diferente de un conjunto de resultados: un conjunto de resultados es el conjunto de filas que coincide con los criterios de búsqueda determinada, mientras que un cursor es el software que devuelve las filas a la aplicación. El nombre *cursor,* tal como se aplica a las bases de datos, probablemente se ha originado el cursor parpadeante en un equipo de terminal. Igual que ese cursor indica la posición actual en la pantalla y donde las palabras con tipo aparecerá siguientes, un cursor en un conjunto de resultados indica la posición actual en el conjunto de resultados y qué filas se devolverán a continuación.  
  
 El modelo de cursor de ODBC se basa en el modelo de cursor en SQL incrustado. Una diferencia importante entre estos modelos es que se abren los cursores de manera. En SQL incrustado, un cursor debe ser explícitamente declarado y abierto antes de poder utilizarlo. En ODBC, implícitamente se abre un cursor cuando se ejecuta una instrucción que crea un conjunto de resultados. Cuando se abre el cursor, se coloca antes de la primera fila del conjunto de resultados. En embedded SQL y ODBC, se debe cerrar un cursor después de la aplicación ha terminado de usarlo.  
  
 Los cursores diferentes tienen características diferentes. El tipo más común de cursor, que se denomina un *cursor de solo avance,* sólo puede desplazarse hacia delante por el conjunto de resultados. Para volver a la fila anterior, la aplicación debe cerrar y volver a abrir el cursor y, a continuación, leer las filas desde el principio del conjunto de resultados hasta que llega a la fila necesaria. Los cursores de avance y solo proporcionan un mecanismo rápido para hacer que un único paso a través de un conjunto de resultados.  
  
 Los cursores de avance y solo son menos útil para aplicaciones basadas en la pantalla, en el que el usuario se desplaza hacia atrás y hacia delante a través de los datos. Tales aplicaciones pueden utilizar un cursor de solo avance, lea el resultado de establecer una vez, almacenamiento en caché los datos localmente y realizar el desplazamiento por sí mismos. Sin embargo, esto funciona bien sólo con pequeñas cantidades de datos. Una solución mejor es usar un *un cursor desplazable,* que proporciona acceso aleatorio al conjunto de resultados. Estas aplicaciones pueden mejorar el rendimiento mediante la captura de más de una fila de datos a la vez, con lo que se denomina un *cursor de bloque.* Para obtener más información acerca de los cursores de bloque, vea [utilizar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 El cursor de sólo avance es el tipo de cursor predeterminado en ODBC y se explica en las secciones siguientes. Para obtener más información acerca de los cursores de bloque y los cursores desplazables, consulte [cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md) y [cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  Confirmar o revertir una transacción, ya sea llamando explícitamente a **SQLEndTran** o funcionando en modo de confirmación automática, hace que algunos orígenes de datos cerrar todos los cursores en todas las instrucciones en una conexión. Para obtener más información, vea los atributos SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.

