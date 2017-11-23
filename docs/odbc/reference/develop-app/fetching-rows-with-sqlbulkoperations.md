---
title: Capturar filas con SQLBulkOperations | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84b8e31821e1571da8272806c5fcd7f5563a4182
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Capturar filas con SQLBulkOperations
Datos pueden ser volver a capturar en un conjunto de filas mediante marcadores mediante una llamada a **SQLBulkOperations.** Las filas que se va a capturar se identifican mediante los marcadores en una columna de marcador enlazado. No se capturan las columnas con un valor de SQL_COLUMN_IGNORE.  
  
 Para realizar capturas de forma masiva con **SQLBulkOperations**, la aplicación hace lo siguiente:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que deben actualizarse. Si hay más de un marcador y se usa el enlace, los marcadores se almacenan en una matriz; Si hay más de un marcador y se usa el enlace de modo de fila, los marcadores se almacenan en una matriz de estructuras de fila.  
  
2.  Establece el atributo de instrucción de SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se va a capturar y enlaza el búfer que contiene el valor de marcador o la matriz de marcadores para la columna 0.  
  
3.  Establece el valor en el búfer de longitud/indicador de cada columna según sea necesario. Se trata de la longitud de bytes de los datos o SQL_NTS de las columnas enlazadas a los búferes de cadena, la longitud de bytes de los datos de las columnas enlazadas a búferes binarios y SQL_NULL_DATA de las columnas que se establece en NULL. La aplicación establece el valor en el búfer de longitud/indicador de las columnas que se van a establecer en su valor predeterminado (si existe) o NULL (si no lo hace) para SQL_COLUMN_IGNORE.  
  
4.  Llamadas **SQLBulkOperations** con el *operación* establecido en SQL_FETCH_BY_BOOKMARK.  
  
 No hay ninguna necesidad de la aplicación para que utilice la matriz de operación de fila para evitar que la operación se realizará en determinadas columnas. La aplicación selecciona las filas que desea capturar copiando sólo los marcadores para las filas en la matriz de marcador enlazado.
