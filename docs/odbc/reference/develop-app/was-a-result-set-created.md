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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db287e729678f54aaf637950c89c724724678f08
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208396"
---
# <a name="was-a-result-set-created"></a>¿Era un conjunto creado de resultados?
En la mayoría de los casos, los programadores de aplicaciones saben si las instrucciones que se ejecuta su aplicación va a crear un conjunto de resultados. Esto sucede si la aplicación usa las instrucciones SQL codificadas de forma rígida escritas por el programador. Normalmente es el caso cuando la aplicación crea instrucciones SQL en tiempo de ejecución: El programador fácilmente puede incluir código que identifica si un **seleccione** instrucción o un **insertar** instrucción se está construyendo. En algunas situaciones, el programador no puede saber si una instrucción creará un conjunto de resultados. Esto es cierto si la aplicación proporciona una forma para el usuario escribir y ejecutar una instrucción SQL. También es true cuando la aplicación crea una instrucción en tiempo de ejecución para ejecutar un procedimiento.  
  
 En tales casos, la aplicación llama a **SQLNumResultCols** para determinar el número de columnas del conjunto de resultados. Si es 0, la instrucción no ha creado un conjunto de resultados; Si es cualquier otro número, la instrucción ha creado un conjunto de resultados.  
  
 La aplicación puede llamar a **SQLNumResultCols** en cualquier momento después de preparación o ejecución de la instrucción. Sin embargo, dado que algunos orígenes de datos no pueden describir con facilidad los conjuntos de resultados que se crearán con instrucciones preparadas, rendimiento se verá afectado si **SQLNumResultCols** se llama después de prepara una instrucción pero antes de ejecutarlo.  
  
 Algunos orígenes de datos también admiten la determinación del número de filas que devuelve una instrucción SQL en un conjunto de resultados. Para ello, la aplicación llama a **SQLRowCount**. Es exactamente lo que representa el recuento de filas indicado por la configuración de la opción SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (según el tipo del cursor) devuelto por una llamada a **SQLGetInfo**. Esta máscara de bits indica para cada tipo de cursor si el recuento de filas devuelto es exacto, aproximado, o no está disponible en absoluto. Si los recuentos de filas para estático o los cursores dinámicos se ven afectados por los cambios realizados a través de **SQLBulkOperations** o **SQLSetPos**, o mediante la actualización por posición o las instrucciones delete, depende de otros bits Devuelve los mismos argumentos opción mencionados anteriormente. Para obtener más información, consulte el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
