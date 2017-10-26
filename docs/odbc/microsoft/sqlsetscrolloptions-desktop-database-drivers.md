---
title: SQLSetScrollOptions (controladores de base de datos de escritorio) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd83d7ce68d0a7bc1045aee76c28b9b5c39c9faf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (controladores de escritorio de la base de datos)
Se admiten cursores estáticos y hacia delante para SQL_CONCUR_READ_ONLY.  
  
 Cursores dinámicos solo son compatibles con un *fConcurrency* argumento de SQL_CONCUR_LOCK.  
  
 Un *fConcurrency* de SQL_CONCUR_ROWVER no se admite.  
  
 No se admiten los cursores dinámicos y cursores mixtos.

