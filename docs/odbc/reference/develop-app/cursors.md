---
description: Cursores (ODBC)
title: Cursores (ODBC) | Microsoft Docs
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
ms.openlocfilehash: 10dbd2517c29bcd02d1d39abe0b2caec1bf03312
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429407"
---
# <a name="odbc-cursors"></a>Cursores ODBC
Una aplicación captura datos con un *cursor*. Un cursor es diferente de un conjunto de resultados: un conjunto de resultados es el conjunto de filas que coincide con criterios de búsqueda determinados, mientras que un cursor es el software que devuelve esas filas a la aplicación. El cursor de nombre *,* tal y como se aplica a las bases de datos, probablemente se originó a partir del cursor parpadeante en un terminal de equipo. Del mismo modo que ese cursor indica la posición actual en la pantalla y dónde aparecerán las palabras escritas después, un cursor en un conjunto de resultados indica la posición actual en el conjunto de resultados y la fila que se devolverá a continuación.  
  
 El modelo de cursor de ODBC se basa en el modelo de cursor de SQL incrustado. Una diferencia importante entre estos modelos es la forma en que se abren los cursores. En SQL incrustado, se debe declarar y abrir explícitamente un cursor antes de poder usarlo. En ODBC, se abre un cursor implícitamente cuando se ejecuta una instrucción que crea un conjunto de resultados. Cuando se abre el cursor, se coloca antes de la primera fila del conjunto de resultados. En SQL incrustado y ODBC, se debe cerrar un cursor después de que la aplicación haya terminado de usarlo.  
  
 Los cursores diferentes tienen características diferentes. El tipo de cursor más común, que se denomina *cursor de solo avance,* solo puede avanzar por el conjunto de resultados. Para volver a una fila anterior, la aplicación debe cerrar y volver a abrir el cursor y, a continuación, leer las filas desde el principio del conjunto de resultados hasta que llegue a la fila requerida. Los cursores de solo avance proporcionan un mecanismo rápido para realizar un solo paso a través de un conjunto de resultados.  
  
 Los cursores de solo avance son menos útiles para las aplicaciones basadas en pantalla, en las que el usuario se desplaza hacia atrás y hacia delante por los datos. Estas aplicaciones pueden usar un cursor de solo avance mediante la lectura de un conjunto de resultados una vez, el almacenamiento en caché de los datos localmente y la realización del desplazamiento. Sin embargo, esto solo funciona bien con pequeñas cantidades de datos. Una solución mejor es usar un *cursor desplazable,* que proporciona acceso aleatorio al conjunto de resultados. Estas aplicaciones también pueden aumentar el rendimiento mediante la captura de más de una fila de datos a la vez, mediante lo que se denomina *cursor de bloque.* Para obtener más información sobre los cursores de bloque, vea [usar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 El cursor de solo avance es el tipo de cursor predeterminado en ODBC y se describe en las secciones siguientes. Para obtener más información sobre los cursores de bloque y los cursores desplazables, consulte [cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md) y [cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  La confirmación o reversión de una transacción, ya sea mediante una llamada explícita a **SQLEndTran** o mediante el funcionamiento en el modo de confirmación automática, hace que algunos orígenes de datos cierren todos los cursores en todas las instrucciones de una conexión. Para obtener más información, vea los atributos SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
