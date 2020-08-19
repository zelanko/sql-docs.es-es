---
description: SQLSpecialColumns (controladores de escritorio de la base de datos)
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
ms.openlocfilehash: d3f023c4f82c5a2f9af7af2e34cc697ffdb34206
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421619"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (controladores de escritorio de la base de datos)
Se devolverá un índice único (si existe) para la marca de SQL_BEST_ROWID en *fColType*. No se devolverá ningún conjunto de resultados para la marca de SQL_ROWVER.  
  
 Todos los identificadores de fila tienen un ámbito de SQL_SCOPE_CURROW.  
  
 No se admite la coincidencia de patrones para el argumento *szTableQualifier* o *szTableName* .
