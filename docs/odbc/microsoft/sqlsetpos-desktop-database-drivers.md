---
description: SQLSetPos (controladores de escritorio de la base de datos)
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
ms.openlocfilehash: 4aa126514bc84f5546e1f4a022d8d3e6235b2e7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421669"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (controladores de escritorio de la base de datos)
Se admite la semántica de modelo masivo para las llamadas a **SQLSetPos** con el argumento *IRow* igual a 0.  
  
 SQL_LOCK_NO_CHANGE es compatible con la *rebaño*. No se admiten SQL_LOCK_EXCLUSIVE y SQL_LOCK_UNLOCK.  
  
 **SQLSetPos** admite combinaciones actualizables. (Para obtener más información, vea la *Guía del programador de Microsoft Jet motor de base de datos*).
