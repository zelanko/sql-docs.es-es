---
description: ¿Era un conjunto creado de resultados?
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
ms.openlocfilehash: 57b65c254f48d9c3f5078c3b2c1f576ae54d4740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421389"
---
# <a name="was-a-result-set-created"></a>¿Era un conjunto creado de resultados?
En la mayoría de los casos, los programadores de aplicaciones saben si las instrucciones que ejecuta la aplicación crearán un conjunto de resultados. Este es el caso si la aplicación usa instrucciones SQL codificadas de forma rígida escritas por el programador. Normalmente, es el caso cuando la aplicación construye instrucciones SQL en tiempo de ejecución: el programador puede incluir fácilmente código que marca si se está construyendo una instrucción **Select** o una instrucción **Insert** . En algunas situaciones, el programador no puede saber si una instrucción creará un conjunto de resultados. Esto es así si la aplicación proporciona una manera para que el usuario escriba y ejecute una instrucción SQL. También se aplica cuando la aplicación crea una instrucción en tiempo de ejecución para ejecutar un procedimiento.  
  
 En tales casos, la aplicación llama a **SQLNumResultCols** para determinar el número de columnas del conjunto de resultados. Si es 0, la instrucción no creó un conjunto de resultados; Si es cualquier otro número, la instrucción crea un conjunto de resultados.  
  
 La aplicación puede llamar a **SQLNumResultCols** en cualquier momento después de preparar o ejecutar la instrucción. Sin embargo, dado que algunos orígenes de datos no pueden describir fácilmente los conjuntos de resultados que se crearán mediante instrucciones preparadas, el rendimiento se verá afectado si se llama a **SQLNumResultCols** después de preparar una instrucción, pero antes de que se ejecute.  
  
 Algunos orígenes de datos también admiten la determinación del número de filas que devuelve una instrucción SQL en un conjunto de resultados. Para ello, la aplicación llama a **SQLRowCount**. La configuración de las opciones SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (según el tipo de cursor) devuelta por una llamada a **SQLGetInfo**indica exactamente lo que representa el recuento de filas. Esta máscara de máscara indica para cada tipo de cursor si el número de filas devuelto es exacto, aproximado o no está disponible en absoluto. El recuento de filas para los cursores estáticos o controlados por conjunto de claves se ve afectado por los cambios realizados a través de **SQLBulkOperations** o **SQLSetPos**, o por las instrucciones UPDATE o DELETE posicionadas, depende de otros bits devueltos por los mismos argumentos de opción enumerados anteriormente. Para obtener más información, vea la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
