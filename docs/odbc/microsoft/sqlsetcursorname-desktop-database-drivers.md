---
title: SQLSetCursorName (controladores de escritorio de la base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e433e6aee341085965f361992fc8ea9ac8744353
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305628"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (controladores de escritorio de la base de datos)
Dado que el controlador no admite una actualización por posición o eliminar el WHERE CURRENT OF *cursorname* sintaxis, **SQLSetCursorName** se admite, pero no se puede usar para las actualizaciones posicionadas. Solo puede usarse cuando se habilita la biblioteca de cursores y la aplicación usa **SQLExtendedFetch**.
