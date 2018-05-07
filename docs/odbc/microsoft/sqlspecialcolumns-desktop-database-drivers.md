---
title: SQLSpecialColumns (controladores de base de datos de escritorio) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aebdcc1d45584ec0fa7d287715e2defc8ef278fb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (controladores de escritorio de la base de datos)
Un índice único se devolverá (si existe) para la marca SQL_BEST_ROWID en *fColType*. No se devolverá ningún conjunto de resultados para la marca SQL_ROWVER.  
  
 Todos los identificadores de fila tienen un ámbito de SQL_SCOPE_CURROW.  
  
 No se admite la coincidencia de patrones para cada uno el *szTableQualifier* o *szTableName* argumento.
