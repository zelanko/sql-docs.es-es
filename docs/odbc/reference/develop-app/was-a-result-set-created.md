---
title: ¿Era un conjunto creado de resultados? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b2701f568397c2a6714587bf4261f5a4295f226
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="was-a-result-set-created"></a>¿Era un conjunto creado de resultados?
En la mayoría de los casos, los programadores de aplicaciones conocer si las instrucciones que se ejecuta la aplicación creará un conjunto de resultados. Esto sucede si la aplicación utiliza las instrucciones SQL codificadas de forma rígida escritas por el programador. Normalmente es el caso cuando la aplicación cree instrucciones SQL en tiempo de ejecución: el programador fácilmente puede incluir código que identifica si una **seleccione** instrucción o un **insertar** instrucción se va a construir. En algunos casos poco frecuentes, el programador no puede saber si una instrucción creará un conjunto de resultados. Esto es cierto si la aplicación proporciona una manera para que el usuario escriba y ejecute una instrucción SQL. También es cierto cuando la aplicación crea una instrucción en tiempo de ejecución para ejecutar un procedimiento.  
  
 En tales casos, la aplicación llama a **SQLNumResultCols** para determinar el número de columnas del conjunto de resultados. Si es 0, la instrucción no ha creado un conjunto de resultados; Si es cualquier otro número, la instrucción ha creado un conjunto de resultados.  
  
 La aplicación puede llamar a **SQLNumResultCols** en cualquier momento después de la preparación o ejecución de la instrucción. Sin embargo, dado que algunos orígenes de datos no pueden describir fácilmente los conjuntos de resultados que se va a crear instrucciones preparadas, rendimiento se resentiría si **SQLNumResultCols** se llama después de prepara una instrucción pero antes de que se ejecute.  
  
 Algunos orígenes de datos también admiten determinar el número de filas devueltas por una instrucción SQL en un conjunto de resultados. Para ello, la aplicación llama **SQLRowCount**. Lo que representa el número de filas indicado por la configuración de la opción SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (dependiendo del tipo del cursor) devuelto por una llamada a **SQLGetInfo**. Esta máscara de bits indica para cada tipo de cursor si el recuento de filas devuelto es exacta, aproximada o no está disponible en absoluto. Si los recuentos de filas para estático o los cursores dinámicos se ven afectados por los cambios realizados a través de **SQLBulkOperations** o **SQLSetPos**, o por actualización por posición o las instrucciones delete, depende de otros elementos Devuelve los mismos argumentos de opción indicados anteriormente. Para obtener más información, consulte el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
