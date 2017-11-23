---
title: SQLSetStmtOption (controladores de base de datos de escritorio) | Documentos de Microsoft
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
helpviewer_keywords: SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 09f5e675ca04c801df89d0ab289d6928c6cd1210
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (controladores de escritorio de la base de datos)
|*fOption*|Comentarios|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|No se admite el procesamiento asincrónico. El fOption SQL_ASYNC_ENABLE devolverá SQLSTATE S1C00 (no compatible con el controlador).|  
|SQL_KEYSET_SIZE|El tamaño del conjunto de claves sólo es válido es 0, dado que combinar y no se admiten los cursores dinámicos. Si este valor se establece en cualquier otro número, se cambiará a 0 y la llamada devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 de SQLState (valor de opción cambiado).|  
|SQL_MAX_ROWS|El tamaño del conjunto de filas solo es válido es 0, dado que los controladores de base de datos de escritorio no admiten la limitación del número de filas que se devuelven. Si este valor se establece en cualquier otro número, se cambiará a 0 y la llamada devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 de SQLState (valor de opción cambiado).|  
|SQL_QUERY_TIMEOUT|No compatible.|  
|SQL_ROW_NUMBER|No compatible.|  
|SQL_SIMULATE_CURSOR|No compatible.|
