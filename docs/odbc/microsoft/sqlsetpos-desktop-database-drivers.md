---
title: SQLSetPos (controladores de base de datos de escritorio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e151e3abc4032ea3180e46360c501d9fbea9ae30
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301466"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (controladores de escritorio de la base de datos)
Se admite la semántica de modelo masivo para las llamadas a **SQLSetPos** con el argumento *IRow* igual a 0.  
  
 SQL_LOCK_NO_CHANGE es compatible con la *rebaño*. No se admiten SQL_LOCK_EXCLUSIVE y SQL_LOCK_UNLOCK.  
  
 **SQLSetPos** admite combinaciones actualizables. (Para obtener más información, vea la *Guía del programador de Microsoft Jet motor de base de datos*).
