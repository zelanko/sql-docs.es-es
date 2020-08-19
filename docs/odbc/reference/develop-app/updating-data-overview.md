---
description: Información general sobre actualización de datos
title: Información general sobre la actualización de datos | Microsoft Docs
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
ms.openlocfilehash: 2b1755ea75426030a96ed7b349cc82f0fc7e282a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424427"
---
# <a name="updating-data-overview"></a>Información general sobre actualización de datos
Las aplicaciones pueden actualizar datos mediante la ejecución de instrucciones SQL o mediante una llamada a **SQLSetPos** o **SQLBulkOperations**. Las instrucciones **Update**, **Delete**e **Insert** actúan directamente en el origen de datos y suelen ser compatibles con los controladores. Las instrucciones Update y DELETE buscadas contienen una especificación de las filas que se van a cambiar. Las instrucciones Update y DELETE posicionadas y **SQLSetPos** actúan en el origen de datos a través de un cursor y se admiten con menos frecuencia.  
  
 El hecho de que los cursores puedan detectar los cambios realizados en el conjunto de resultados con los métodos descritos en esta sección depende del tipo de cursor y de cómo se implemente. Los cursores de solo avance no vuelven a visitar las filas y, por tanto, no detectan ningún cambio. Para obtener información sobre si los cursores desplazables pueden detectar cambios, vea [cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Las instrucciones INSERT, DELETE y UPDATE](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Actualización posicionada y las instrucciones Delete](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simulación de actualización por posición y las instrucciones Delete](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Actualizar datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Actualizar datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Datos de tipo Long y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
