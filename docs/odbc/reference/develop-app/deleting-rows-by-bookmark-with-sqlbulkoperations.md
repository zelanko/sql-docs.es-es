---
title: Eliminar filas por marcador con SQLBulkOperations | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db7e04c5bf76855afdb24676c905c5cccbc60cbc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Eliminar filas por marcador con SQLBulkOperations
Cuando se elimina una fila por marcador, **SQLBulkOperations** hace que el origen de datos elimine una o más filas seleccionadas de la tabla. Las filas se identifican mediante el marcador en una columna de marcador enlazado.  
  
 Para eliminar filas por marcador con **SQLBulkOperations**, la aplicación hace lo siguiente:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que va a eliminar. Si hay más de un marcador y se usa el enlace, los marcadores se almacenan en una matriz; Si hay más de un marcador y se usa el enlace de modo de fila, los marcadores se almacenan en una matriz de estructuras de fila.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de marcadores y enlaza el búfer que contiene el valor de marcador o la matriz de marcadores para la columna 0.  
  
3.  Llamadas **SQLBulkOperations** con *operación* establecido en SQL_DELETE_BY_BOOKMARK.

