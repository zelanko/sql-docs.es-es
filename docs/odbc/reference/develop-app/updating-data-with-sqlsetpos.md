---
title: Actualizar datos con SQLSetPos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286165"
---
# <a name="updating-data-with-sqlsetpos"></a>Actualizar datos con SQLSetPos
Las aplicaciones pueden actualizar o eliminar cualquier fila del conjunto de filas con **SQLSetPos**. Llamar a **SQLSetPos** es una alternativa práctica para construir y ejecutar una instrucción SQL. Permite que un controlador ODBC admita actualizaciones posicionadas incluso cuando el origen de datos no admite instrucciones SQL colocadas. Forma parte del paradigma de lograr el acceso completo a la base de datos por medio de llamadas a funciones.  
  
 **SQLSetPos** funciona en el conjunto de filas actual y solo se puede usar después de una llamada a **SQLFetchScroll**. La aplicación especifica el número de la fila que se va a actualizar, eliminar o insertar, y el controlador recupera los nuevos datos de esa fila de los búferes del conjunto de filas. **SQLSetPos** también se puede utilizar para designar una fila especificada como la fila actual o para actualizar una fila determinada del conjunto de filas desde el origen de datos.  
  
 El tamaño del conjunto de filas se establece mediante una llamada a **SQLSetStmtAttr** con un argumento de *atributo* de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** usa un nuevo tamaño de conjunto de filas, sin embargo, solo después de una llamada a **SQLFetch** o **SQLFetchScroll**. Por ejemplo, si se cambia el tamaño del conjunto de filas, se llama a **SQLSetPos** y luego se llama a **SQLFetch** o **sqlfetchscroll** , y la llamada a **SQLSetPos** utiliza el tamaño del conjunto de filas anterior, mientras que **SQLFetch** o **sqlfetchscroll** usa el nuevo tamaño del conjunto de filas.  
  
 La primera fila del conjunto de filas es el número de fila 1. El argumento *RowNumber* de **SQLSetPos** debe identificar una fila del conjunto de filas; es decir, su valor debe estar en el intervalo comprendido entre 1 y el número de filas que se capturaron más recientemente (que puede ser menor que el tamaño del conjunto de filas). Si *RowNumber* es 0, la operación se aplica a todas las filas del conjunto de filas.  
  
 Dado que la mayor parte de la interacción con bases de datos relacionales se realiza a través de SQL, **SQLSetPos** no es ampliamente compatible. Sin embargo, un controlador puede emularla fácilmente mediante la creación y ejecución de una instrucción **Update** o **Delete** .  
  
 Para determinar qué operaciones admite **SQLSetPos** , una aplicación llama a **SQLGetInfo** con la opción de información SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (dependiendo del tipo de cursor).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Actualizar las filas del conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Eliminación de filas en el conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
