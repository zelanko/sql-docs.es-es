---
title: SQLStatistics (controlador de acceso) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f75f41bf63cbf224772955effa0f120b5d384111
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299365"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|La ruta de acceso a un archivo de base de datos se devuelve para Microsoft Access.<br /><br /> La coincidencia de patrones no se admite en el argumento *szTableQualifier.*|  
|TABLE_OWNER|NULL se devuelve en esta columna, porque no se admite el nombre de propietario.|  
|TABLE_NAME|Nombre de tabla no delimitado.<br /><br /> La coincidencia de patrones no se admite en el *argumento szTableName.*|  
|INDEX_QUALIFIER|NULL siempre se devuelve.|  
|INDEX_NAME|Depende del índice.|  
|TYPE|Solo se devolverán SQL_TABLE_STAT o SQL_INDEX_OTHER para TYPE.|  
|SEQ_IN_INDEX|Depende del índice.|  
|COLUMN_NAME|Depende del índice.|  
|COLLATION|Depende del índice.|  
|CARDINALITY|Se devuelve solo para Microsoft Access.|  
|PAGES|NULL siempre se devuelve.|  
  
 El filtrado se basa en la unicidad (el argumento *fUnique).* Se omite el parámetro *fAccuracy.*
