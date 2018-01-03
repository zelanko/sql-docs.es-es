---
title: SQLSpecialColumns (controladores de base de datos de escritorio) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5292e86e32c495f2491826e74105b9d23e39328
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (controladores de escritorio de la base de datos)
Un índice único se devolverá (si existe) para la marca SQL_BEST_ROWID en *fColType*. No se devolverá ningún conjunto de resultados para la marca SQL_ROWVER.  
  
 Todos los identificadores de fila tienen un ámbito de SQL_SCOPE_CURROW.  
  
 No se admite la coincidencia de patrones para cada uno el *szTableQualifier* o *szTableName* argumento.
