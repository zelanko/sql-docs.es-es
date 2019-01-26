---
title: SQLSetStmtOption (controladores de escritorio de la base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48dc5dff83e942b894548d44e3673c19ca0746c5
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044878"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (controladores de escritorio de la base de datos)

|*fOption*|Comentarios|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|No se admite el procesamiento asincrónico. FOption SQL_ASYNC_ENABLE devolverá SQLSTATE S1C00 (no compatible con el controlador).|  
|SQL_KEYSET_SIZE|El tamaño del conjunto de claves sólo es válido es 0, dado que combinar y no se admiten los cursores dinámicos. Si este valor se establece en cualquier otro número, se cambiará en 0 y la llamada devolverá SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 de SQLState (valor de opción cambiado).|  
|SQL_MAX_ROWS|El tamaño del conjunto de filas sólo es válido es 0, dado que los controladores de base de datos de escritorio no admiten la limitación del número de filas que se devuelven. Si este valor se establece en cualquier otro número, se cambiará en 0 y la llamada devolverá SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 de SQLState (valor de opción cambiado).|  
|SQL_QUERY_TIMEOUT|No compatible.|  
|SQL_ROW_NUMBER|No compatible.|  
|SQL_SIMULATE_CURSOR|No compatible.|
