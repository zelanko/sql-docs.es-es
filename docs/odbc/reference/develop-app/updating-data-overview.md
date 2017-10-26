---
title: "Actualizar información general sobre datos | Documentos de Microsoft"
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
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3da35917f3979b041d6eb5b61d6554d4ef4c4585
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updating-data-overview"></a>Información general sobre actualización de datos
Las aplicaciones pueden actualizar los datos mediante la ejecución de instrucciones SQL o mediante una llamada a **SQLSetPos** o **SQLBulkOperations**. **ACTUALIZACIÓN**, **eliminar**, y **insertar** instrucciones actúan directamente en el origen de datos y normalmente son compatibles con los controladores. Buscar actualizaciones y las instrucciones delete contienen una especificación de las filas que se va a cambiar. Actualización por posición e instrucciones delete y **SQLSetPos** actúe en el origen de datos a través de un cursor y son menos ampliamente compatibles.  
  
 Si los cursores pueden detectar los cambios realizados en el conjunto de resultados con los métodos descritos en esta sección depende del tipo de cursor y cómo se implementa. Cursores de solo avance no volver a visitar filas y, por tanto, no detectará los cambios. Para obtener información acerca de si los cursores desplazables pueden detectar cambios, consulte [cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Las instrucciones INSERT, DELETE y UPDATE](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Actualización posicionada y las instrucciones Delete](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simulación de actualización por posición y las instrucciones Delete](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Actualizar datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Actualizar datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Datos de tipo Long y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)

