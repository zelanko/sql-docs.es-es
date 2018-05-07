---
title: SQLSetScrollOptions (controladores de base de datos de escritorio) | Documentos de Microsoft
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
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5838e890168473cd70d957eb1da6d4be45f546dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (controladores de escritorio de la base de datos)
Se admiten cursores estáticos y hacia delante para SQL_CONCUR_READ_ONLY.  
  
 Cursores dinámicos solo son compatibles con un *fConcurrency* argumento de SQL_CONCUR_LOCK.  
  
 Un *fConcurrency* de SQL_CONCUR_ROWVER no se admite.  
  
 No se admiten los cursores dinámicos y cursores mixtos.
