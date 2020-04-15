---
title: Actualización de datos con SQLSetPos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16476a1e1007905f34ec2e70ce6032eb8d81fe7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286165"
---
# <a name="updating-data-with-sqlsetpos"></a>Actualizar datos con SQLSetPos
Las aplicaciones pueden actualizar o eliminar cualquier fila del conjunto de filas con **SQLSetPos**. Llamar a **SQLSetPos** es una alternativa conveniente para construir y ejecutar una instrucción SQL. Permite que un controlador ODBC admita actualizaciones posicionadas incluso cuando el origen de datos no admite instrucciones SQL posicionadas. Es parte del paradigma de lograr el acceso completo a la base de datos mediante llamadas de función.  
  
 **SQLSetPos** funciona en el conjunto de filas actual y solo se puede usar después de una llamada a **SQLFetchScroll**. La aplicación especifica el número de la fila que se va a actualizar, eliminar o insertar y el controlador recupera los nuevos datos de esa fila de los búferes del conjunto de filas. **SQLSetPos** también se puede usar para designar una fila especificada como la fila actual o para actualizar una fila determinada en el conjunto de filas desde el origen de datos.  
  
 El tamaño del conjunto de filas se establece mediante una llamada a **SQLSetStmtAttr** con un *argumento Attribute* de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** utiliza un nuevo tamaño de conjunto de filas, sin embargo, sólo después de una llamada a **SQLFetch** o **SQLFetchScroll**. Por ejemplo, si se cambia el tamaño del conjunto de filas, **SQLSetPos** se llama y, a continuación, **SQLFetch** o **SQLFetchScroll** se llama y la llamada a **SQLSetPos** usa el tamaño de conjunto de filas antiguo mientras **SQLFetch** o **SQLFetchScroll** usa el nuevo tamaño de conjunto de filas.  
  
 La primera fila del conjunto de filas es el número de fila 1. El *RowNumber* argumento en **SQLSetPos** debe identificar una fila en el conjunto de filas; es decir, su valor debe estar entre 1 y el número de filas que se capturaron más recientemente (que puede ser menor que el tamaño del conjunto de filas). Si *RowNumber* es 0, la operación se aplica a todas las filas del conjunto de filas.  
  
 Dado que la mayor parte de la interacción con bases de datos relacionales se realiza a través de SQL, **SQLSetPos** no es ampliamente compatible. Sin embargo, un controlador puede emularlo fácilmente mediante la construcción y ejecución de una instrucción **UPDATE** o **DELETE.**  
  
 Para determinar qué operaciones admite **SQLSetPos,** una aplicación llama a **SQLGetInfo** con la opción de información SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (según el tipo del cursor).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Actualizar las filas del conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Eliminación de filas en el conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
