---
title: "Eliminación de filas en el conjunto de filas con SQLSetPos | Documentos de Microsoft"
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
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac33a8370cbd76a3dde43df68c12c9417fc78e07
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Eliminación de filas en el conjunto de filas con SQLSetPos
La operación de eliminación de **SQLSetPos** hace que el origen de datos elimine una o más filas seleccionadas de una tabla. Para eliminar filas con **SQLSetPos**, la aplicación llama **SQLSetPos** con *operación* establecido en SQL_DELETE y *RowNumber* establecido en el número de la fila que se va a eliminar. Si *RowNumber* es 0, se eliminan todas las filas del conjunto de filas.  
  
 Después de **SQLSetPos** devuelve la fila eliminada es la fila actual y su estado es SQL_ROW_DELETED. La fila no se puede usar en las operaciones más posicionadas, como llamadas a **SQLGetData** o **SQLSetPos**.  
  
 Al eliminar todas las filas del conjunto de filas (*RowNumber* es igual a 0), la aplicación puede impedir que el controlador elimine determinadas filas utilizando la matriz de operación de fila, en la misma forma que para la operación de actualización de **SQLSetPos** . (Consulte [actualizar las filas del conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Cada fila que se elimina debe ser una fila que exista en el conjunto de resultados. Si se rellenaron los búferes de la aplicación y se ha mantenido una matriz de Estados de fila, sus valores en cada una de estas posiciones de fila no deben ser SQL_ROW_DELETED, SQL_ROW_ERROR ni SQL_ROW_NOROW.

