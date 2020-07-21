---
title: SQLSetScrollOptions (controladores de base de datos de escritorio) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c47255b455354c49133d61c3546be63ab2380a1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299444"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (controladores de escritorio de la base de datos)
Los cursores forward y Static se admiten para SQL_CONCUR_READ_ONLY.  
  
 Solo se admiten cursores controlados por conjunto de claves para un argumento *fConcurrency* de SQL_CONCUR_LOCK.  
  
 No se admite un argumento *fConcurrency* de SQL_CONCUR_ROWVER.  
  
 No se admiten los cursores dinámicos ni los de mezcla.
