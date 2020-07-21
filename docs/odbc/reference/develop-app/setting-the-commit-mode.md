---
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
ms.openlocfilehash: f05aaca2349a612cda7c5b6b257e7a1d5a5ea9c5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299825"
---
# <a name="setting-the-commit-mode"></a>Establecer el modo de confirmación
Las aplicaciones especifican el modo de transacción con el SQL_ATTR_AUTOCOMMIT atributo de conexión. De forma predeterminada, las transacciones ODBC están en modo de confirmación automática (a menos que no se admitan **SQLSetConnectAttr** y **SQLSetConnectOption** , lo que es improbable). El cambio del modo de confirmación manual al modo de confirmación automática confirma automáticamente cualquier transacción abierta en la conexión.
