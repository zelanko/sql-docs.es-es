---
title: Marcar filas en ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7f2d19fe6cf79e11c11a5e6c5c4839ae35788353
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109239"
---
# <a name="bookmarking-rows-in-odbc"></a>Marcar filas en ODBC
  Un marcador es un valor utilizado para identificar una fila de datos. El significado del valor de marcador solamente lo conocen el controlador u origen de datos. Por ejemplo, podría ser tan simple como un número de fila o tan complejo como una dirección de disco. En ODBC, la aplicación solicita un marcador para una fila determinada, lo almacena y lo pasa de vuelta al cursor para volver a la fila.  
  
 Al capturar filas con [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md), una aplicación puede utilizar un marcador como base para la selección de la fila inicial. Ésta es una forma de dirección absoluta porque no depende de la posición actual del cursor. Para desplazarse a una fila marcada, la aplicación llama **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_BOOKMARK. Esta operación utiliza el marcador al que señala el atributo de opción SQL_ATTR_FETCH_BOOKMARK_PTR. Devuelve el conjunto de filas que comienza con la fila identificada por este marcador. Una aplicación puede especificar un desplazamiento para esta operación en el *FetchOffset* argumento de la llamada a **SQLFetchScroll**. Cuando se especifica un desplazamiento, la primera fila del conjunto de filas devuelto se determina sumando el número del argumento FetchOffset al número de la fila que identifica el marcador. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client solamente admite marcadores en los cursores estáticos y controlados por conjunto de claves. Si se solicita un cursor dinámico cuando los marcadores están activados, se abre un cursor controlado por conjunto de claves.  
  
 También pueden utilizar marcadores con el **SQLBulkOperations** función para realizar operaciones en un conjunto de filas que comienza en el marcador.  
  
## <a name="see-also"></a>Vea también  
 [Desplazamiento y captura de filas](../native-client-ole-db-rowsets/fetching-rows.md)  
  
  