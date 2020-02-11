---
title: SQLSetStmtOption (controladores de base de datos de escritorio) | Microsoft Docs
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
ms.openlocfilehash: 20043c96771bf888defa2c8fbeb028aaa18f5abc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905343"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (controladores de escritorio de la base de datos)

|*fOption*|Comentarios|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|No se admite el procesamiento asincrónico. El SQL_ASYNC_ENABLE fOption devolverá SQLSTATE S1C00 (controlador no compatible).|  
|SQL_KEYSET_SIZE|El único tamaño de conjunto de claves válido es 0, ya que no se admiten los cursores mixtos y dinámicos. Si este valor se establece en cualquier otro número, se cambiará a 0 y la llamada devolverá SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 (valor de opción cambiado).|  
|SQL_MAX_ROWS|El único tamaño de conjunto de filas válido es 0, ya que los controladores de base de datos de escritorio no admiten limitar el número de filas que se devuelven. Si este valor se establece en cualquier otro número, se cambiará a 0 y la llamada devolverá SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 (valor de opción cambiado).|  
|SQL_QUERY_TIMEOUT|No compatible.|  
|SQL_ROW_NUMBER|No compatible.|  
|SQL_SIMULATE_CURSOR|No compatible.|
