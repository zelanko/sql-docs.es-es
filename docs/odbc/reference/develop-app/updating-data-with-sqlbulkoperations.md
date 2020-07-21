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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b96e3a43b8385910e4260cf51dea7e4ff508200
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298489"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Actualizar datos con SQLBulkOperations
Las aplicaciones pueden realizar operaciones de actualización masiva, eliminación, recuperación o inserción en la tabla subyacente en el origen de datos con una llamada a **SQLBulkOperations**. Llamar a **SQLBulkOperations** es una alternativa práctica para construir y ejecutar una instrucción SQL. Permite que un controlador ODBC admita actualizaciones posicionadas incluso cuando el origen de datos no admite instrucciones SQL colocadas. Forma parte del paradigma de lograr el acceso completo a la base de datos por medio de llamadas a funciones.  
  
 **SQLBulkOperations** funciona en el conjunto de filas actual y solo se puede usar después de una llamada a **SQLFetch** o **SQLFetchScroll**. La aplicación especifica las filas que se van a actualizar, eliminar o actualizar mediante el almacenamiento en caché de sus marcadores. El controlador recupera los nuevos datos de las filas que se van a actualizar, o los nuevos datos que se van a insertar en la tabla subyacente, de los búferes del conjunto de filas.  
  
 El tamaño del conjunto de filas que va a usar **SQLBulkOperations** se establece mediante una llamada a **SQLSetStmtAttr** con un argumento de *atributo* de SQL_ATTR_ROW_ARRAY_SIZE. A diferencia de **SQLSetPos**, que usa un nuevo tamaño del conjunto de filas solo después de una llamada a **SQLFetch** o **SQLFetchScroll**, **SQLBulkOperations** usa el nuevo tamaño del conjunto de filas después de la llamada a **SQLSetStmtAttr**.  
  
 Dado que la mayor parte de la interacción con bases de datos relacionales se realiza a través de SQL, **SQLBulkOperations** no se admite ampliamente. Sin embargo, un controlador puede emularla fácilmente mediante la creación y ejecución de una instrucción **Update**, **Delete**o **Insert** .  
  
 Para determinar qué operaciones admite **SQLBulkOperation** , una aplicación llama a **SQLGetInfo** con la opción de información SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (dependiendo del tipo de cursor).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Actualizar las filas por marcador con SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Eliminar filas por marcador con SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Insertar filas con SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Capturar filas con SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
