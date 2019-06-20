---
title: SQLSetPos (controladores de escritorio de la base de datos) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95117c82c213851d2e0600e65d8061ce532d9933
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200456"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (controladores de escritorio de la base de datos)
La semántica del modelo de forma masiva para **SQLSetPos** llama con el *irow* argumento igual a 0 se admiten.  
  
 Es compatible con SQL_LOCK_NO_CHANGE *manada*. No se admiten SQL_LOCK_EXCLUSIVE y SQL_LOCK_UNLOCK.  
  
 **SQLSetPos** admite combinaciones actualizables. (Para obtener más información, consulte el *Guía del programador del motor de base de datos Jet de Microsoft*.)
