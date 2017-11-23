---
title: SQLStatistics (controlador de acceso) | Documentos de Microsoft
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
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a2def3a3ada57a085779701269af569554a4f76
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|Se devuelve la ruta de acceso a un archivo de base de datos de Microsoft Access.<br /><br /> No se admite la coincidencia de patrones en los *szTableQualifier* argumento.|  
|TABLE_OWNER|Se devuelve NULL en esta columna, porque no se admite el nombre del propietario.|  
|TABLE_NAME|Nombre de la tabla no delimitado.<br /><br /> No se admite la coincidencia de patrones en los *szTableName* argumento.|  
|INDEX_QUALIFIER|Siempre devuelve NULL.|  
|INDEX_NAME|Dependientes del índice.|  
|TYPE|Se devolverá solo SQL_TABLE_STAT o SQL_INDEX_OTHER para el tipo.|  
|SEQ_IN_INDEX|Dependientes del índice.|  
|COLUMN_NAME|Dependientes del índice.|  
|COLLATION|Dependientes del índice.|  
|CARDINALITY|Solo se devuelve para Microsoft Access.|  
|PAGES|Siempre devuelve NULL.|  
  
 El filtrado se basa en unicidad (la *fUnique* argumento). El *fAccuracy* parámetro se ignora.
