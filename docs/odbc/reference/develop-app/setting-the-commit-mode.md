---
description: Establecer el modo de confirmación
title: Establecer el modo de confirmación | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a71d6f97f4683f9177c940be7d6ca1cc4a27c01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494629"
---
# <a name="setting-the-commit-mode"></a>Establecer el modo de confirmación
Las aplicaciones especifican el modo de transacción con el SQL_ATTR_AUTOCOMMIT atributo de conexión. De forma predeterminada, las transacciones ODBC están en modo de confirmación automática (a menos que no se admitan **SQLSetConnectAttr** y **SQLSetConnectOption** , lo que es improbable). El cambio del modo de confirmación manual al modo de confirmación automática confirma automáticamente cualquier transacción abierta en la conexión.
