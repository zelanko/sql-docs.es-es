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
manager: craigg
ms.openlocfilehash: e74a3207691aca001dcf334c1ee50d53d4f34d69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305698"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (controladores de escritorio de la base de datos)
Se admiten cursores estáticos y hacia delante para SQL_CONCUR_READ_ONLY.  
  
 Los cursores dinámicos solo son compatibles con un *fConcurrency* argumento de SQL_CONCUR_LOCK.  
  
 Un *fConcurrency* no se admite el argumento de SQL_CONCUR_ROWVER.  
  
 No se admiten los cursores dinámicos y cursores mixtos.
