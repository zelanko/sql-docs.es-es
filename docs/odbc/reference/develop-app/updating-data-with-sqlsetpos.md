---
title: Actualizar datos con SQLSetPos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb89d4a2220c487f2e126b50ecf8cbedd20857cc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updating-data-with-sqlsetpos"></a>Actualizar datos con SQLSetPos
Las aplicaciones pueden actualizar o eliminar cualquier fila del conjunto de filas con **SQLSetPos**. Al llamar a **SQLSetPos** es una buena alternativa para crear y ejecutar una instrucción SQL. Permite que un controlador ODBC admite actualizaciones por posición incluso cuando el origen de datos no admite las instrucciones SQL posicionadas. Forma parte del paradigma de lograr acceso a la base de datos completa por medio de llamadas a funciones.  
  
 **SQLSetPos** opera en el conjunto de filas actual y puede usarse solo después de llamar a **SQLFetchScroll**. La aplicación especifica el número de la fila para actualizar, eliminar o insertar, y el controlador recupera los nuevos datos de esa fila de los búferes de conjunto de filas. **SQLSetPos** también puede usarse para designar una fila especificada como la fila actual, o para actualizar una fila determinada en el conjunto de filas del origen de datos.  
  
 Tamaño de conjunto de filas se establece mediante una llamada a **SQLSetStmtAttr** con una *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** usa un nuevo tamaño de conjunto de filas, sin embargo, solo después de llamar a **SQLFetch** o **SQLFetchScroll**. Por ejemplo, si se cambia el tamaño de conjunto de filas, **SQLSetPos** se llama y, a continuación, **SQLFetch** o **SQLFetchScroll** se llama y la llamada a **SQLSetPos** utiliza el tamaño de conjunto de filas anterior al **SQLFetch** o **SQLFetchScroll** utiliza el nuevo tamaño del conjunto de filas.  
  
 La primera fila del conjunto de filas es el número de fila 1. El *RowNumber* argumento en **SQLSetPos** debe identificar una fila del conjunto de filas; es decir, su valor debe ser entre 1 y el número de filas que se han capturado recientemente (lo que puede ser menor que tamaño de conjunto de filas). Si *RowNumber* es 0, la operación se aplica a todas las filas del conjunto de filas.  
  
 Puesto que la mayoría de interacción con bases de datos relacionales se realiza a través de SQL, **SQLSetPos** no se admite ampliamente. Sin embargo, un controlador puede fácilmente emular, crear y ejecutar un **actualización** o **eliminar** instrucción.  
  
 Para determinar qué operaciones **SQLSetPos** admite, una aplicación llama **SQLGetInfo** con el SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 opción de información (según el tipo del cursor).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Actualizar las filas del conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Eliminación de filas en el conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)

