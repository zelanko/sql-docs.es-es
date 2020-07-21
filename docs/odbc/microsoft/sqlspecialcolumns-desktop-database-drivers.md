---
title: SQLSpecialColumns (controladores de base de datos de escritorio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f8cd4ed0912f9f1e71d64b32449b5d46f9ef1a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299395"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (controladores de escritorio de la base de datos)
Se devolverá un índice único (si existe) para la marca de SQL_BEST_ROWID en *fColType*. No se devolverá ningún conjunto de resultados para la marca de SQL_ROWVER.  
  
 Todos los identificadores de fila tienen un ámbito de SQL_SCOPE_CURROW.  
  
 No se admite la coincidencia de patrones para el argumento *szTableQualifier* o *szTableName* .
