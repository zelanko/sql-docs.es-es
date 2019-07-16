---
title: SQLSetScrollOptions (controladores de escritorio de la base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0adedfb69cd4a7b5cf195916747687826805e8bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905389"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (controladores de escritorio de la base de datos)
Se admiten cursores estáticos y hacia delante para SQL_CONCUR_READ_ONLY.  
  
 Los cursores dinámicos solo son compatibles con un *fConcurrency* argumento de SQL_CONCUR_LOCK.  
  
 Un *fConcurrency* no se admite el argumento de SQL_CONCUR_ROWVER.  
  
 No se admiten los cursores dinámicos y cursores mixtos.
