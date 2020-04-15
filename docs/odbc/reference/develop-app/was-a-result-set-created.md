---
title: ¿Era un conjunto creado de resultados? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c171a154dd16a291c5dbe1dcade8c01ea95fb084
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294553"
---
# <a name="was-a-result-set-created"></a>¿Era un conjunto creado de resultados?
En la mayoría de las situaciones, los programadores de aplicaciones saben si las instrucciones que ejecuta su aplicación crearán un conjunto de resultados. Este es el caso si la aplicación utiliza instrucciones SQL codificadas de forma rígida escritas por el programador. Suele ser el caso cuando la aplicación construye instrucciones SQL en tiempo de ejecución: el programador puede incluir fácilmente código que marca si se está construyendo una instrucción **SELECT** o una instrucción **INSERT.** En algunas situaciones, el programador no puede saber si una instrucción creará un conjunto de resultados. Esto es cierto si la aplicación proporciona una manera para que el usuario escriba y ejecute una instrucción SQL. También es true cuando la aplicación construye una instrucción en tiempo de ejecución para ejecutar un procedimiento.  
  
 En estos casos, la aplicación llama a **SQLNumResultCols** para determinar el número de columnas del conjunto de resultados. Si es 0, la instrucción no creó un conjunto de resultados; si es cualquier otro número, la instrucción creó un conjunto de resultados.  
  
 La aplicación puede llamar a **SQLNumResultCols** en cualquier momento después de preparar o ejecutar la instrucción. Sin embargo, dado que algunos orígenes de datos no pueden describir fácilmente los conjuntos de resultados que se crearán mediante instrucciones preparadas, el rendimiento se verá afectado si se llama a **SQLNumResultCols** después de preparar una instrucción pero antes de que se ejecute.  
  
 Algunos orígenes de datos también admiten la determinación del número de filas que devuelve una instrucción SQL en un conjunto de resultados. Para ello, la aplicación llama a **SQLRowCount**. Exactamente lo que representa el recuento de filas se indica mediante la configuración de la SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 opción (dependiendo del tipo del cursor) devuelta por una llamada a **SQLGetInfo**. Esta máscara de bits indica para cada tipo de cursor si el recuento de filas devuelto es exacto, aproximado o no está disponible en absoluto. Si los recuentos de filas para cursores estáticos o controlados por conjuntos de claves se ven afectados por los cambios realizados a través de **SQLBulkOperations** o **SQLSetPos**, o por instrucciones de actualización o eliminación posicionadas, depende de otros bits devueltos por los mismos argumentos de opción enumerados anteriormente. Para obtener más información, vea la descripción de la función [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
