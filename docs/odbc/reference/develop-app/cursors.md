---
title: Cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91765f0572d8c880f7505948f7756b373fe28f62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042131"
---
# <a name="cursors"></a>Cursores
Una aplicación recupera los datos con un *cursor*. Un cursor es diferente de un conjunto de resultados: Un conjunto de resultados es el conjunto de filas que coincide con los criterios de búsqueda determinado, mientras que un cursor es el software que devuelve las filas a la aplicación. El nombre *cursor,* tal como se aplica a bases de datos, probablemente se ha originado el cursor parpadeante en un equipo de terminal. Igual que ese cursor indica la posición actual en la pantalla y donde las palabras con tipo aparecerá siguientes, un cursor en un conjunto de resultados indica la posición actual en el conjunto de resultados y qué fila se devolverá a continuación.  
  
 El modelo de cursor de ODBC se basa en el modelo de cursor en SQL incrustado. Una diferencia importante entre estos modelos es que se abren los cursores de forma. En SQL incrustado, un cursor debe estar explícitamente declarado y abierto antes de poder usarlo. En ODBC, implícitamente se abre un cursor cuando se ejecuta una instrucción que crea un conjunto de resultados. Cuando se abre el cursor, se coloca antes de la primera fila del conjunto de resultados. En embedded SQL y ODBC, se debe cerrar un cursor después de la aplicación termina de usarla.  
  
 Los cursores diferentes tienen características diferentes. El tipo más común de cursor, lo que se denomina un *cursor de solo avance,* sólo puede desplazarse hacia delante por el conjunto de resultados. Para volver a una fila anterior, la aplicación debe cerrar y volver a abrir el cursor y, a continuación, leer las filas desde el principio del conjunto hasta que alcanza la fila requiere de resultados. Cursores de solo avance proporcionan un mecanismo rápido para realizar un único paso a través de un conjunto de resultados.  
  
 Cursores de solo avance son menos útil para aplicaciones basadas en la pantalla, en el que el usuario se desplaza hacia atrás y hacia delante a través de los datos. Estas aplicaciones pueden utilizar un cursor de solo avance, lea el resultado de establecer una vez, almacenamiento en caché los datos localmente y la realización de desplazamiento a sí mismos. Sin embargo, esto funciona bien únicamente con pequeñas cantidades de datos. Una solución mejor es usar un *cursor desplazable,* que proporciona acceso aleatorio al conjunto de resultados. Estas aplicaciones pueden también aumentar el rendimiento mediante la captura de más de una fila de datos a la vez, con lo que se denomina un *cursor de bloque.* Para obtener más información acerca de los cursores de bloque, consulte [utilizar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 El cursor de solo avance es el tipo de cursor predeterminado en ODBC y se explica en las secciones siguientes. Para obtener más información acerca de los cursores de bloque y los cursores desplazables, consulte [cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md) y [los cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  Confirmar o revertir una transacción, ya sea llamando explícitamente **SQLEndTran** o al operar en modo de confirmación automática, hace que algunos orígenes de datos cerrar todos los cursores en todas las instrucciones en una conexión. Para obtener más información, vea los atributos SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
