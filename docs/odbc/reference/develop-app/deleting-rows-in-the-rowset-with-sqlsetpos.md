---
title: Eliminación de filas en el conjunto de filas con SQLSetPos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940bcc3e2ee6a042394797d6038028cce64862f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305956"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Eliminación de filas en el conjunto de filas con SQLSetPos
La operación de eliminación de **SQLSetPos** hace que el origen de datos elimine una o varias filas seleccionadas de una tabla. Para eliminar filas con **SQLSetPos**, la aplicación llama a **SQLSetPos** con *Operation* establecido en SQL_DELETE y *RowNumber* establecido en el número de la fila que se van a eliminar. Si *RowNumber* es 0, se eliminan todas las filas del conjunto de filas.  
  
 Después de **SQLSetPos** devuelve, la fila eliminada es la fila actual y su estado es SQL_ROW_DELETED. La fila no se puede utilizar en otras operaciones posicionadas, como llamadas a **SQLGetData** o **SQLSetPos**.  
  
 Al eliminar todas las filas del conjunto de filas (*RowNumber* es igual a 0), la aplicación puede impedir que el controlador eliminar determinadas filas mediante la matriz de operaciones de fila, de la misma manera que para la operación de actualización de **SQLSetPos**. (Consulte [Actualización de filas en el conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Cada fila que se elimina debe ser una fila que exista en el conjunto de resultados. Si los búferes de aplicación se llenaron mediante la obtención y si se ha mantenido una matriz de estado de fila, sus valores en cada una de estas posiciones de fila no deben ser SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW.
