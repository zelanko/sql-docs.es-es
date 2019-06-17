---
title: Actualizar las filas por marcador con SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9f0c59324542793301965c7d3555cf35ad40f5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194396"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Actualizar las filas por marcador con SQLBulkOperations
Al actualizar una fila por marcador, **SQLBulkOperations** hace que el origen de datos a actualizar una o varias filas de la tabla. Las filas se identifican mediante el marcador en una columna de marcador enlazado. La fila se actualiza con los datos en los búferes de la aplicación para cada columna enlazada (excepto cuando el valor en el búfer de longitud/indicador para una columna es SQL_COLUMN_IGNORE). No se actualizará las columnas sin enlazar.  
  
 Para actualizar filas por marcador con **SQLBulkOperations**, la aplicación:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que deben actualizarse. Si hay más de un marcador y se usa el enlace, los marcadores se almacenan en una matriz. Si hay más de un marcador y se usa el enlace, los marcadores se almacenan en una matriz de estructuras de fila.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de marcadores y enlaza el búfer que contiene el valor de marcador o la matriz de marcadores para la columna 0.  
  
3.  Coloca los nuevos valores de datos en los búferes de conjunto de filas. Para obtener información sobre cómo enviar datos largos con **SQLBulkOperations**, consulte [datos de tipo Long y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Establece el valor en el búfer de longitud/indicador de cada columna según sea necesario. Se trata de la longitud de bytes de los datos o SQL_NTS para las columnas enlazadas a los búferes de cadena, la longitud de bytes de los datos para las columnas enlazadas a los búferes de binarios y SQL_NULL_DATA para las columnas debe establecerse en NULL.  
  
5.  Establece el valor en el búfer de longitud/indicador de esas columnas que no se puede actualizar a SQL_COLUMN_IGNORE. Aunque la aplicación puede omitir este paso y reenviar los datos existentes, esto resulta ineficaz y corre el riesgo de enviar los valores al origen de datos que se han truncado durante su lectura.  
  
6.  Las llamadas **SQLBulkOperations** con el *operación* establecido en SQL_UPDATE_BY_BOOKMARK.  
  
 Para cada fila que se envía al origen de datos como una actualización, los búferes de la aplicación deben tener datos de fila válida. Si se han rellenado los búferes de la aplicación mediante la captura, si se ha mantenido una matriz de Estados de fila, y si el valor de estado para una fila es SQL_ROW_DELETED, SQL_ROW_ERROR ni SQL_ROW_NOROW, datos no válidos sin darse cuenta podrían enviarse al origen de datos.
