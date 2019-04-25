---
title: Actualizar datos con SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 958514adc02452cdc75a05e7ad28cd31f4e8e0e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632448"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Actualizar datos con SQLBulkOperations
Las aplicaciones pueden realizar operaciones de actualización, eliminación, fetch o inserción masiva en la tabla subyacente en el origen de datos con una llamada a **SQLBulkOperations**. Una llamada a **SQLBulkOperations** es una buena alternativa para crear y ejecutar una instrucción SQL. Permite que un controlador ODBC admiten las actualizaciones posicionadas incluso cuando el origen de datos no admite instrucciones SQL posicionadas. Es parte del paradigma de conseguir acceso a la base de datos completa por medio de las llamadas de función.  
  
 **SQLBulkOperations** opera en el conjunto de filas actual y se puede usar solo después de llamar a **SQLFetch** o **SQLFetchScroll**. La aplicación especifica las filas para actualizar, eliminar o actualizar al almacenar en caché sus marcadores. El controlador recupera los nuevos datos de filas que deben actualizarse o los nuevos datos que va a insertar en la tabla subyacente, de los búferes de conjunto de filas.  
  
 El tamaño del conjunto de filas que va a usar **SQLBulkOperations** se establece mediante una llamada a **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. A diferencia de **SQLSetPos**, que usa un nuevo tamaño del conjunto de filas sólo después de llamar a **SQLFetch** o **SQLFetchScroll**, **SQLBulkOperations** usa la nuevo tamaño del conjunto de filas después de llamar a **SQLSetStmtAttr**.  
  
 Dado que la mayoría de interacción con bases de datos relacionales se realiza a través de SQL, **SQLBulkOperations** no se admite ampliamente. Sin embargo, un controlador puede fácilmente emular, crear y ejecutar un **actualización**, **eliminar**, o **insertar** instrucción.  
  
 Para determinar qué operaciones **SQLBulkOperation** admite, una aplicación llama a **SQLGetInfo** con el SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR _ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 información opción (según el tipo del cursor).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Actualizar las filas por marcador con SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Eliminar filas por marcador con SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Insertar filas con SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Capturar filas con SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
