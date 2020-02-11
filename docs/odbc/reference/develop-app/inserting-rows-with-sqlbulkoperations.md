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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138922"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Insertar filas con SQLBulkOperations
La inserción de datos con **SQLBulkOperations** es similar a la actualización de datos con **SQLBulkOperations** porque usa datos de los búferes de la aplicación enlazada.  
  
 Para que cada columna de la nueva fila tenga un valor, todas las columnas enlazadas con un valor de longitud/indicador de SQL_COLUMN_IGNORE y todas las columnas sin enlazar deben aceptar valores NULL o tener un valor predeterminado.  
  
 Para insertar filas con **SQLBulkOperations**, la aplicación hace lo siguiente:  
  
1.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se van a insertar y coloca los nuevos valores de datos en los búferes de la aplicación enlazada. Para obtener información sobre cómo enviar datos largos con **SQLBulkOperations**, consulte [Long Data y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Establece el valor del búfer de longitud/indicador de cada columna según sea necesario. Es la longitud de bytes de los datos o SQL_NTS para las columnas enlazadas a búferes de cadena, la longitud de bytes de los datos para las columnas enlazadas a búferes binarios y SQL_NULL_DATA para que las columnas se establezcan en NULL. La aplicación establece el valor del búfer de longitud/indicador de las columnas que se van a establecer en su valor predeterminado (si existe) o NULL (si no hay ninguno) para SQL_COLUMN_IGNORE.  
  
3.  Llama a **SQLBulkOperations** con el argumento *Operation* establecido en SQL_ADD.  
  
 Una vez que **SQLBulkOperations** devuelve, la fila actual no cambia. Si la columna de marcador (columna 0) está enlazada, **SQLBulkOperations** devuelve los marcadores de las filas insertadas en el búfer del conjunto de filas enlazado a esa columna.
