---
description: SQLSetStmtOption (controladores de escritorio de la base de datos)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0696ee98dd88f1c23120ef1d96c6e8d93751f76e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449157"
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
