---
title: Eliminación de filas por marcador con SQLBulkOperations ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b6a4c1b24ee276c86175392eb45ac5ce0aa45e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305966"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Eliminar filas por marcador con SQLBulkOperations
Al eliminar una fila por marcador, **SQLBulkOperations** hace que el origen de datos elimine una o varias filas seleccionadas de la tabla. Las filas se identifican mediante el marcador en una columna de marcador enlazado.  
  
 Para eliminar filas por marcador con **SQLBulkOperations**, la aplicación hace lo siguiente:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que se van a eliminar. Si hay más de un marcador y se utiliza el enlace de columna, los marcadores se almacenan en una matriz; si hay más de un marcador y se utiliza el enlace de fila, los marcadores se almacenan en una matriz de estructuras de fila.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de marcadores y enlaza el búfer que contiene el valor del marcador, o la matriz de marcadores, a la columna 0.  
  
3.  Llama a **SQLBulkOperations** con *Operation* establecido en SQL_DELETE_BY_BOOKMARK.
