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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da899e4dc47daff03c31277b3edd4d9c642b87cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305296"
---
# <a name="cursors"></a>Cursores
Una aplicación recupera datos con un *cursor.* Un cursor es diferente de un conjunto de resultados: un conjunto de resultados es el conjunto de filas que coincide con determinados criterios de búsqueda, mientras que un cursor es el software que devuelve esas filas a la aplicación. El cursor de *nombre,* tal como se aplica a las bases de datos, probablemente se originó a partir del cursor parpadeante en un terminal de equipo. Al igual que ese cursor indica la posición actual en la pantalla y dónde aparecerán las palabras escritas a continuación, un cursor en un conjunto de resultados indica la posición actual en el conjunto de resultados y qué fila se devolverá a continuación.  
  
 El modelo de cursor en ODBC se basa en el modelo de cursor en SQL incrustado. Una diferencia notable entre estos modelos es la forma en que se abren los cursores. En SQL incrustado, un cursor debe declararse y abrirse explícitamente antes de que se pueda usar. En ODBC, un cursor se abre implícitamente cuando se ejecuta una instrucción que crea un conjunto de resultados. Cuando se abre el cursor, se coloca antes de la primera fila del conjunto de resultados. En SQL incrustado y ODBC, un cursor debe cerrarse después de que la aplicación haya terminado de usarlo.  
  
 Diferentes cursores tienen características diferentes. El tipo más común de cursor, que se denomina *cursor de solo avance,* solo puede avanzar a través del conjunto de resultados. Para volver a una fila anterior, la aplicación debe cerrar y volver a abrir el cursor y, a continuación, leer filas desde el principio del conjunto de resultados hasta que llegue a la fila necesaria. Los cursores de solo avance proporcionan un mecanismo rápido para realizar una sola pasada a través de un conjunto de resultados.  
  
 Los cursores de solo avance son menos útiles para aplicaciones basadas en pantalla, en las que el usuario se desplaza hacia atrás y hacia delante a través de los datos. Estas aplicaciones pueden utilizar un cursor de solo avance leyendo el conjunto de resultados una vez, almacenando en caché los datos localmente y realizando el desplazamiento ellos mismos. Sin embargo, esto funciona bien sólo con pequeñas cantidades de datos. Una mejor solución es utilizar un *cursor desplazable,* que proporciona acceso aleatorio al conjunto de resultados. Estas aplicaciones también pueden aumentar el rendimiento mediante la obtención de más de una fila de datos a la vez, utilizando lo que se denomina un cursor de *bloque.* Para obtener más información acerca de los cursores de bloque, consulte Uso de [cursores](../../../odbc/reference/develop-app/using-block-cursors.md)de bloque .  
  
 El cursor de solo avance es el tipo de cursor predeterminado en ODBC y se describe en las secciones siguientes. Para obtener más información sobre los cursores de bloque y los cursores desplazables, vea [Cursores](../../../odbc/reference/develop-app/block-cursors.md) de bloque y [cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  La confirmación o reversión de una transacción, ya sea llamando explícitamente a **SQLEndTran** o operando en modo de confirmación automática, hace que algunos orígenes de datos cierren todos los cursores en todas las instrucciones de una conexión. Para obtener más información, vea los atributos SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en la descripción de la función [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
