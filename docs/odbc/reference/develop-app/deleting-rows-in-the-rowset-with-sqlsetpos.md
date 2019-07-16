---
title: Eliminar filas del conjunto de filas con SQLSetPos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e39b70f92f7b239b011cdd4fdd6abd36c27561c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076804"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Eliminación de filas en el conjunto de filas con SQLSetPos
La operación de eliminación de **SQLSetPos** hace que el origen de datos de eliminar una o varias filas seleccionadas de una tabla. Para eliminar filas con **SQLSetPos**, la aplicación llama a **SQLSetPos** con *operación* establecido en SQL_DELETE y *RowNumber* establecido en el número de la fila a eliminar. Si *RowNumber* es 0, se eliminan todas las filas del conjunto de filas.  
  
 Después de **SQLSetPos** devuelve la fila eliminada es la fila actual y su estado es SQL_ROW_DELETED. La fila no se puede usar en cualquier operación posicionada aún más, como las llamadas a **SQLGetData** o **SQLSetPos**.  
  
 Al eliminar todas las filas del conjunto de filas (*RowNumber* es igual a 0), la aplicación puede impedir que el controlador elimine determinadas filas utilizando la matriz de operación de fila, en la misma manera que la operación de actualización de **SQLSetPos** . (Consulte [actualizar las filas del conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Cada fila que se elimina debe ser una fila que exista en el conjunto de resultados. Si se han rellenado los búferes de la aplicación mediante la captura y se ha mantenido una matriz de Estados de fila, sus valores en cada una de estas posiciones de fila no deben ser SQL_ROW_DELETED, SQL_ROW_ERROR ni SQL_ROW_NOROW.
