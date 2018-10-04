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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1c31ef622281b4f52f62ca3867c5afa7dcae8ca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680793"
---
# <a name="updating-data-with-sqlsetpos"></a>Actualizar datos con SQLSetPos
Pueden actualizar o eliminar cualquier fila del conjunto de filas con las aplicaciones **SQLSetPos**. Una llamada a **SQLSetPos** es una buena alternativa para crear y ejecutar una instrucción SQL. Permite que un controlador ODBC admiten las actualizaciones posicionadas incluso cuando el origen de datos no admite instrucciones SQL posicionadas. Es parte del paradigma de conseguir acceso a la base de datos completa por medio de las llamadas de función.  
  
 **SQLSetPos** opera en el conjunto de filas actual y se puede usar solo después de llamar a **SQLFetchScroll**. La aplicación especifica el número de la fila para actualizar, eliminar o insertar, y el controlador recupera los nuevos datos para esa fila de los búferes de conjunto de filas. **SQLSetPos** también se puede usar para designar una fila especificada como la fila actual, o actualizar una fila determinada en el conjunto de filas del origen de datos.  
  
 Tamaño del conjunto de filas se establece mediante una llamada a **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** usa un nuevo tamaño del conjunto de filas, sin embargo, solo después de llamar a **SQLFetch** o **SQLFetchScroll**. Por ejemplo, si se cambia el tamaño del conjunto de filas, **SQLSetPos** se llama y, a continuación, **SQLFetch** o **SQLFetchScroll** se llama a y la llamada a **SQLSetPos** utiliza el tamaño del conjunto de filas anterior al **SQLFetch** o **SQLFetchScroll** usa el nuevo tamaño del conjunto de filas.  
  
 La primera fila del conjunto de filas es el número de fila 1. El *RowNumber* argumento en **SQLSetPos** debe identificar una fila del conjunto de filas; es decir, su valor debe ser en el intervalo comprendido entre 1 y el número de filas que se han capturado recientemente (lo que puede ser menor que tamaño del conjunto de filas). Si *RowNumber* es 0, la operación se aplica a todas las filas del conjunto de filas.  
  
 Dado que la mayoría de interacción con bases de datos relacionales se realiza a través de SQL, **SQLSetPos** no se admite ampliamente. Sin embargo, un controlador puede fácilmente emular, crear y ejecutar un **actualización** o **eliminar** instrucción.  
  
 Para determinar qué operaciones **SQLSetPos** admite, una aplicación llama a **SQLGetInfo** con el SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 información opción (según el tipo del cursor).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Actualizar las filas del conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Eliminación de filas en el conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
