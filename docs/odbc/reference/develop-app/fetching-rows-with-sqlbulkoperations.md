---
title: Capturar filas con SQLBulkOperations | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a99592210ff315db026d60b8743d4a3bca13c969
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791543"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Capturar filas con SQLBulkOperations
Datos pueden ser volver a capturar en un conjunto de filas mediante marcadores mediante una llamada a **SQLBulkOperations.** Las filas que se capturará se identifican mediante los marcadores en una columna de marcador enlazado. Las columnas con un valor de SQL_COLUMN_IGNORE no se han recuperado.  
  
 Para realizar recuperaciones de forma masiva con **SQLBulkOperations**, la aplicación hace lo siguiente:  
  
1.  Recupera y almacena en caché los marcadores de todas las filas que deben actualizarse. Si hay más de un marcador y se usa el enlace, los marcadores se almacenan en una matriz. Si hay más de un marcador y se usa el enlace, los marcadores se almacenan en una matriz de estructuras de fila.  
  
2.  Establece el atributo de instrucción de SQL_ATTR_ROW_ARRAY_SIZE en el número de filas para capturar y enlaza el búfer que contiene el valor de marcador o la matriz de marcadores para la columna 0.  
  
3.  Establece el valor en el búfer de longitud/indicador de cada columna según sea necesario. Se trata de la longitud de bytes de los datos o SQL_NTS para las columnas enlazadas a los búferes de cadena, la longitud de bytes de los datos para las columnas enlazadas a los búferes de binarios y SQL_NULL_DATA para las columnas debe establecerse en NULL. La aplicación establece el valor en el búfer de longitud/indicador de las columnas que se van a establecerse en sus valores predeterminados (si existe) o NULL (si no lo hace) para SQL_COLUMN_IGNORE.  
  
4.  Las llamadas **SQLBulkOperations** con el *operación* establecido en SQL_FETCH_BY_BOOKMARK.  
  
 No hay ninguna necesidad de la aplicación para usar la matriz de operación de fila para evitar que la operación que se realizará en determinadas columnas. La aplicación selecciona las filas que desea capturar copiando sólo los marcadores para las filas en la matriz dependiente del marcador.
