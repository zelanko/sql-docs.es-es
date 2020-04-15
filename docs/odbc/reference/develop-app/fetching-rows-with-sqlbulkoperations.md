---
title: Obtención de filas con SQLBulkOperations ? Microsoft Docs
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
ms.openlocfilehash: ae0b4c2114059cecaaf8f8825169300f131bd473
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305654"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Capturar filas con SQLBulkOperations
Los datos se pueden convertir en un conjunto de filas mediante marcadores mediante una llamada a **SQLBulkOperations.** Las filas que se van a capturar se identifican mediante los marcadores de una columna de marcador enlazada. Las columnas con un valor de SQL_COLUMN_IGNORE no se recuperan.  
  
 Para realizar recuperaciones masivas con **SQLBulkOperations**, la aplicación hace lo siguiente:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que se van a actualizar. Si hay más de un marcador y se utiliza el enlace de columna, los marcadores se almacenan en una matriz; si hay más de un marcador y se utiliza el enlace de fila, los marcadores se almacenan en una matriz de estructuras de fila.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se van a capturar y enlaza el búfer que contiene el valor del marcador, o la matriz de marcadores, en la columna 0.  
  
3.  Establece el valor en el búfer de longitud/indicador de cada columna según sea necesario. Esta es la longitud de bytes de los datos o SQL_NTS de las columnas enlazadas a búferes de cadena, la longitud de bytes de los datos de las columnas enlazadas a búferes binarios y SQL_NULL_DATA para que las columnas se establezcan en NULL. La aplicación establece el valor en el búfer de longitud/indicador de las columnas que se deben establecer en su valor predeterminado (si existe) o NULL (si no lo hace) en SQL_COLUMN_IGNORE.  
  
4.  Llama a **SQLBulkOperations** con el *Operación* argumento establecido en SQL_FETCH_BY_BOOKMARK.  
  
 No es necesario que la aplicación utilice la matriz de operaciones de fila para evitar que la operación se realice en determinadas columnas. La aplicación selecciona las filas que desea capturar copiando solo los marcadores de esas filas en la matriz de marcadores enlazados.
