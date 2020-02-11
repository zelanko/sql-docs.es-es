---
title: Actualizar filas por marcador con SQLBulkOperations | Microsoft Docs
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
ms.openlocfilehash: e9b10037883ef9cfa4051195270e6477c5cc04ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091623"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Actualizar las filas por marcador con SQLBulkOperations
Al actualizar una fila por marcador, **SQLBulkOperations** hace que el origen de datos actualice una o más filas de la tabla. Las filas se identifican mediante el marcador de una columna de marcador enlazada. La fila se actualiza con los datos de los búferes de la aplicación para cada columna enlazada (excepto cuando el valor del búfer de longitud/indicador de una columna es SQL_COLUMN_IGNORE). No se actualizarán las columnas sin enlazar.  
  
 Para actualizar filas por marcador con **SQLBulkOperations**, la aplicación:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que se van a actualizar. Si se usa más de un marcador y un enlace de modo de columna, los marcadores se almacenan en una matriz; Si se usa más de un marcador y un enlace de modo de fila, los marcadores se almacenan en una matriz de estructuras de filas.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de marcadores y enlaza el búfer que contiene el valor de marcador, o la matriz de marcadores, a la columna 0.  
  
3.  Coloca los nuevos valores de datos en los búferes del conjunto de filas. Para obtener información sobre cómo enviar datos largos con **SQLBulkOperations**, consulte [Long Data y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Establece el valor del búfer de longitud/indicador de cada columna según sea necesario. Es la longitud de bytes de los datos o SQL_NTS para las columnas enlazadas a búferes de cadena, la longitud de bytes de los datos para las columnas enlazadas a búferes binarios y SQL_NULL_DATA para que las columnas se establezcan en NULL.  
  
5.  Establece el valor del búfer de longitud/indicador de las columnas que no se van a actualizar a SQL_COLUMN_IGNORE. Aunque la aplicación puede omitir este paso y volver a enviar los datos existentes, no es eficaz y los riesgos envían valores al origen de datos que se truncaron cuando se leyeron.  
  
6.  Llama a **SQLBulkOperations** con el argumento *Operation* establecido en SQL_UPDATE_BY_BOOKMARK.  
  
 Para cada fila que se envía al origen de datos como una actualización, los búferes de la aplicación deben tener datos de fila válidos. Si los búferes de la aplicación se rellenaron mediante la captura, si se ha mantenido una matriz de estado de fila y si el valor de estado de una fila es SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW, los datos no válidos pueden enviarse accidentalmente al origen de datos.
