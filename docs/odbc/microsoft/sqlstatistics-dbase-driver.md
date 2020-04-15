---
title: SQLStatistics (controlador dBASE) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLStatistics function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLStatistics
ms.assetid: 631cec1b-66b7-4103-b9a7-ffd81da3c442
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: deec1d7cff9ea1d0f8560b3c9b866cad79e69a25
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299355"
---
# <a name="sqlstatistics-dbase-driver"></a>SQLStatistics (dBASE controlador)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador dBASE. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|La ruta de acceso a un directorio.<br /><br /> La coincidencia de patrones no se admite en el argumento *szTableQualifier.*|  
|TABLE_OWNER|NULL se devuelve en esta columna porque no se admite el nombre del propietario.|  
|TABLE_NAME|Nombre de tabla no delimitado.<br /><br /> La coincidencia de patrones no se admite en el *argumento szTableName.*|  
|INDEX_QUALIFIER|NULL siempre se devuelve.|  
|INDEX_NAME|Depende del índice.|  
|TYPE|Solo se devolverán SQL_TABLE_STAT o SQL_INDEX_OTHER para TYPE.|  
|SEQ_IN_INDEX|Depende del índice.|  
|COLUMN_NAME|Depende del índice.|  
|COLLATION|Depende del índice.|  
|PAGES|NULL siempre se devuelve.|  
  
 El filtrado se basa en la unicidad (el argumento *fUnique).* Se omite el parámetro *fAccuracy.*
