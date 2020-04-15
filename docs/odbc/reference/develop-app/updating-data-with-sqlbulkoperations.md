---
title: Actualización de datos con SQLBulkOperations ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298489"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Actualizar datos con SQLBulkOperations
Las aplicaciones pueden realizar operaciones de actualización masiva, eliminación, obtención o inserción en la tabla subyacente en el origen de datos con una llamada a **SQLBulkOperations**. Llamar a **SQLBulkOperations** es una alternativa conveniente para construir y ejecutar una instrucción SQL. Permite que un controlador ODBC admita actualizaciones posicionadas incluso cuando el origen de datos no admite instrucciones SQL posicionadas. Es parte del paradigma de lograr el acceso completo a la base de datos mediante llamadas de función.  
  
 **SQLBulkOperations** funciona en el conjunto de filas actual y solo se puede usar después de una llamada a **SQLFetch** o **SQLFetchScroll**. La aplicación especifica las filas que se van a actualizar, eliminar o actualizar almacenando en caché sus marcadores. El controlador recupera los nuevos datos de las filas que se van a actualizar o los nuevos datos que se insertarán en la tabla subyacente, de los búferes del conjunto de filas.  
  
 El tamaño del conjunto de filas que usará **SQLBulkOperations** se establece mediante una llamada a **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. A diferencia de **SQLSetPos**, que usa un nuevo tamaño de conjunto de filas solo después de una llamada a **SQLFetch** o **SQLFetchScroll**, **SQLBulkOperations** usa el nuevo tamaño de conjunto de filas después de la llamada a **SQLSetStmtAttr**.  
  
 Dado que la mayor parte de la interacción con bases de datos relacionales se realiza a través de SQL, **SQLBulkOperations** no es ampliamente compatible. Sin embargo, un controlador puede emularlo fácilmente construyendo y ejecutando una instrucción **UPDATE**, **DELETE**o **INSERT.**  
  
 Para determinar qué operaciones admite **SQLBulkOperation,** una aplicación llama a **SQLGetInfo** con la opción de información SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (según el tipo del cursor).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Actualizar las filas por marcador con SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Eliminar filas por marcador con SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Insertar filas con SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Capturar filas con SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
