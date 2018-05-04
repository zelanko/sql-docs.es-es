---
title: SQLSpecialColumns (controladores de base de datos de escritorio) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2d2bfda1bb8732e3036c3803628bbe8247f9e76
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (controladores de escritorio de la base de datos)
Un índice único se devolverá (si existe) para la marca SQL_BEST_ROWID en *fColType*. No se devolverá ningún conjunto de resultados para la marca SQL_ROWVER.  
  
 Todos los identificadores de fila tienen un ámbito de SQL_SCOPE_CURROW.  
  
 No se admite la coincidencia de patrones para cada uno el *szTableQualifier* o *szTableName* argumento.
