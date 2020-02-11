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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a43a78ad9453f65d9b12595851bd622f720b409a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094224"
---
# <a name="setting-the-commit-mode"></a>Establecer el modo de confirmación
Las aplicaciones especifican el modo de transacción con el SQL_ATTR_AUTOCOMMIT atributo de conexión. De forma predeterminada, las transacciones ODBC están en modo de confirmación automática (a menos que no se admitan **SQLSetConnectAttr** y **SQLSetConnectOption** , lo que es improbable). El cambio del modo de confirmación manual al modo de confirmación automática confirma automáticamente cualquier transacción abierta en la conexión.
