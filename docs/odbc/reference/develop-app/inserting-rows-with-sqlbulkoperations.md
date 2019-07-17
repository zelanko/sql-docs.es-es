---
title: Insertar filas con SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05b8f71d6f4c885c7dc64887dd92b1f600005ca7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138922"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Insertar filas con SQLBulkOperations
Insertar datos con **SQLBulkOperations** es similar a la actualización de datos con **SQLBulkOperations** porque utiliza datos de los búferes de aplicación enlazadas.  
  
 Para que cada columna de la nueva fila tiene un valor, todas las columnas con un valor de longitud/indicador de SQL_COLUMN_IGNORE enlazadas y todas las columnas sin enlazar deben aceptar valores NULL o tener un valor predeterminado.  
  
 Insertar filas con **SQLBulkOperations**, la aplicación hace lo siguiente:  
  
1.  Establece el atributo de instrucción de SQL_ATTR_ROW_ARRAY_SIZE en el número de filas para insertar y coloca los nuevos valores de datos en los búferes de aplicación enlazadas. Para obtener información sobre cómo enviar datos largos con **SQLBulkOperations**, consulte [datos de tipo Long y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Establece el valor en el búfer de longitud/indicador de cada columna según sea necesario. Se trata de la longitud de bytes de los datos o SQL_NTS para las columnas enlazadas a los búferes de cadena, la longitud de bytes de los datos para las columnas enlazadas a los búferes de binarios y SQL_NULL_DATA para las columnas debe establecerse en NULL. La aplicación establece el valor en el búfer de longitud/indicador de las columnas que se van a establecerse en sus valores predeterminados (si existe) o NULL (si no lo hace) para SQL_COLUMN_IGNORE.  
  
3.  Las llamadas **SQLBulkOperations** con el *operación* establecido en SQL_ADD.  
  
 Después de **SQLBulkOperations** devuelve, no se ha modificado la fila actual. Si está enlazada la columna de marcador (columna 0), **SQLBulkOperations** devuelve los marcadores de las filas insertadas en el búfer del conjunto de filas enlazados a esa columna.
