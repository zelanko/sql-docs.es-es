---
title: Actualización de filas por marcador con SQLBulkOperations ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c755297e8beadad92b5be81d78ca534bb96ecae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283203"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Actualizar las filas por marcador con SQLBulkOperations
Al actualizar una fila por marcador, **SQLBulkOperations** hace que el origen de datos actualice una o varias filas de la tabla. Las filas se identifican mediante el marcador en una columna de marcador enlazado. La fila se actualiza utilizando datos en los búferes de aplicación para cada columna enlazada (excepto cuando el valor del búfer de longitud/indicador para una columna es SQL_COLUMN_IGNORE). Las columnas sin enlazar no se actualizarán.  
  
 Para actualizar filas por marcador con **SQLBulkOperations**, la aplicación:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que se van a actualizar. Si hay más de un marcador y se utiliza el enlace de columna, los marcadores se almacenan en una matriz; si hay más de un marcador y se utiliza el enlace de fila, los marcadores se almacenan en una matriz de estructuras de fila.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de marcadores y enlaza el búfer que contiene el valor del marcador, o la matriz de marcadores, a la columna 0.  
  
3.  Coloca los nuevos valores de datos en los búferes del conjunto de filas. Para obtener información sobre cómo enviar datos largos con **SQLBulkOperations**, vea [Long Data y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Establece el valor en el búfer de longitud/indicador de cada columna según sea necesario. Esta es la longitud de bytes de los datos o SQL_NTS de las columnas enlazadas a búferes de cadena, la longitud de bytes de los datos de las columnas enlazadas a búferes binarios y SQL_NULL_DATA para que las columnas se establezcan en NULL.  
  
5.  Establece el valor en el búfer de longitud/indicador de las columnas que no se deben actualizar a SQL_COLUMN_IGNORE. Aunque la aplicación puede omitir este paso y reenviar los datos existentes, esto es ineficaz y corre el riesgo de enviar valores al origen de datos que se truncaron cuando se leyeron.  
  
6.  Llama a **SQLBulkOperations** con el *Operación* argumento establecido en SQL_UPDATE_BY_BOOKMARK.  
  
 Para cada fila que se envía al origen de datos como una actualización, los búferes de aplicación deben tener datos de fila válidos. Si los búferes de aplicación se rellenaron mediante la obtención, si se ha mantenido una matriz de estado de fila y si el valor de estado de una fila es SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW, los datos no válidos podrían enviarse inadvertidamente al origen de datos.
