---
description: Eliminación de filas en el conjunto de filas con SQLSetPos
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42b61aa9af15526420b6f2d4ef7e8c945e0da105
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476777"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Eliminación de filas en el conjunto de filas con SQLSetPos
La operación de eliminación de **SQLSetPos** hace que el origen de datos elimine una o varias filas seleccionadas de una tabla. Para eliminar filas con **SQLSetPos**, la aplicación llama a **SQLSetPos** con la *operación* establecida en SQL_DELETE y *RowNumber* establecida en el número de la fila que se va a eliminar. Si *RowNumber* es 0, se eliminan todas las filas del conjunto de filas.  
  
 Una vez que **SQLSetPos** devuelve, la fila eliminada es la fila actual y su estado es SQL_ROW_DELETED. La fila no se puede usar en ninguna otra operación posicionada, como las llamadas a **SQLGetData** o **SQLSetPos**.  
  
 Al eliminar todas las filas del conjunto de filas (*RowNumber* es igual a 0), la aplicación puede evitar que el controlador elimine determinadas filas mediante la matriz de operaciones de fila, de la misma forma que para la operación de actualización de **SQLSetPos**. (Vea [Actualizar filas en el conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)).  
  
 Cada fila que se elimina debe ser una fila que exista en el conjunto de resultados. Si los búferes de la aplicación se rellenaron mediante la captura y se ha mantenido una matriz de estado de fila, sus valores en cada una de estas posiciones de fila no deben ser SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW.
