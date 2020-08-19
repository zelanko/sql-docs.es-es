---
description: SQLSetScrollOptions (controladores de escritorio de la base de datos)
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
ms.openlocfilehash: 57237aca0a68119f6ab8f967b9641f2a2a52fc8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421649"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (controladores de escritorio de la base de datos)
Los cursores forward y Static se admiten para SQL_CONCUR_READ_ONLY.  
  
 Solo se admiten cursores controlados por conjunto de claves para un argumento *fConcurrency* de SQL_CONCUR_LOCK.  
  
 No se admite un argumento *fConcurrency* de SQL_CONCUR_ROWVER.  
  
 No se admiten los cursores dinámicos ni los de mezcla.
