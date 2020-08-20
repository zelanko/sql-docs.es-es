---
description: Capturar filas con SQLBulkOperations
title: Capturando filas con SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4c3cb6a38e3ef9c42f4e853b8c406579b5c0236
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499875"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Capturar filas con SQLBulkOperations
Los datos se pueden volver a capturar en un conjunto de filas mediante marcadores mediante una llamada a **SQLBulkOperations.** Las filas que se van a capturar se identifican mediante los marcadores de una columna de marcador enlazada. No se capturan las columnas con un valor de SQL_COLUMN_IGNORE.  
  
 Para realizar capturas masivas con **SQLBulkOperations**, la aplicación hace lo siguiente:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que se van a actualizar. Si se usa más de un marcador y un enlace de modo de columna, los marcadores se almacenan en una matriz; Si se usa más de un marcador y un enlace de modo de fila, los marcadores se almacenan en una matriz de estructuras de filas.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se van a capturar y enlazar el búfer que contiene el valor de marcador, o la matriz de marcadores, a la columna 0.  
  
3.  Establece el valor del búfer de longitud/indicador de cada columna según sea necesario. Es la longitud de bytes de los datos o SQL_NTS para las columnas enlazadas a búferes de cadena, la longitud de bytes de los datos para las columnas enlazadas a búferes binarios y SQL_NULL_DATA para que las columnas se establezcan en NULL. La aplicación establece el valor del búfer de longitud/indicador de las columnas que se van a establecer en su valor predeterminado (si existe) o NULL (si no hay ninguno) para SQL_COLUMN_IGNORE.  
  
4.  Llama a **SQLBulkOperations** con el argumento *Operation* establecido en SQL_FETCH_BY_BOOKMARK.  
  
 No es necesario que la aplicación use la matriz de operaciones de fila para evitar que la operación se realice en determinadas columnas. La aplicación selecciona las filas que desea capturar copiando solo los marcadores de esas filas en la matriz de marcadores enlazada.
