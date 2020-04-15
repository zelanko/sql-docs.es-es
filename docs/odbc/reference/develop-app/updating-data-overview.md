---
title: Descripción general de los datos de actualización de datos Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9972ab61f041385ae4ca616df093ae63ad7a47d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300391"
---
# <a name="updating-data-overview"></a>Información general sobre actualización de datos
Las aplicaciones pueden actualizar los datos ejecutando instrucciones SQL o llamando a **SQLSetPos** o **SQLBulkOperations**. **Las**instrucciones UPDATE , **DELETE**e **INSERT** actúan directamente en el origen de datos y normalmente son compatibles con los controladores. Las instrucciones de actualización y eliminación buscadas contienen una especificación de las filas que se van a cambiar. Las instrucciones update y delete posicionadas y **SQLSetPos** actúan en el origen de datos a través de un cursor y son menos ampliamente compatibles.  
  
 Si los cursores pueden detectar los cambios realizados en el conjunto de resultados con los métodos descritos en esta sección depende del tipo del cursor y de cómo se implemente. Los cursores de solo avance no vuelven a visitar filas y, por lo tanto, no detectarán ningún cambio. Para obtener información sobre si los cursores desplazables pueden detectar [cambios, consulte Cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Las instrucciones INSERT, DELETE y UPDATE](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Actualización posicionada y las instrucciones Delete](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simulación de actualización por posición y las instrucciones Delete](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Actualizar datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Actualizar datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Datos de tipo Long y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
