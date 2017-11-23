---
title: SQLStatistics (controlador de archivo de texto) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Text File Driver
ms.assetid: 311afc01-d656-425f-be43-4a8e7cbc9a97
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9309adf4839c4450d14ba00ed3338d7b70371254
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlstatistics-text-file-driver"></a>SQLStatistics (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|La ruta de acceso a un directorio.<br /><br /> No se admite la coincidencia de patrones en los *szTableQualifier* argumento.|  
|TABLE_OWNER|Se devuelve NULL en esta columna porque no se admite el nombre del propietario.|  
|TABLE_NAME|Nombre de la tabla no delimitado.<br /><br /> No se admite la coincidencia de patrones en los *szTableName* argumento.|  
|INDEX_QUALIFIER|Siempre devuelve NULL.|  
|INDEX_NAME|Dependientes del índice.|  
|TYPE|Se devolverá solo SQL_TABLE_STAT o SQL_INDEX_OTHER para el tipo.|  
|SEQ_IN_INDEX|Dependientes del índice.|  
|COLUMN_NAME|Dependientes del índice.|  
|COLLATION|Dependientes del índice.|  
|PAGES|Siempre devuelve NULL.|  
  
 El filtrado se basa en unicidad (la *fUnique* argumento). El *fAccuracy* parámetro se ignora.
