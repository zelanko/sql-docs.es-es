---
title: SQLStatistics (Controlador de archivo de texto) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Text File Driver
ms.assetid: 311afc01-d656-425f-be43-4a8e7cbc9a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 76b9810236b4ec415f8abb8ecefca748c13b51c8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299315"
---
# <a name="sqlstatistics-text-file-driver"></a>SQLStatistics (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
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
