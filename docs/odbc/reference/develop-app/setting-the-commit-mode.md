---
title: "Establecer el modo de confirmación | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27119d632e62a7f45635062d913360dd59f29c7e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="setting-the-commit-mode"></a>Establecer el modo de confirmación
Las aplicaciones especificar el modo de transacción con el atributo de conexión SQL_ATTR_AUTOCOMMIT. De forma predeterminada, las transacciones de ODBC están en modo de confirmación automática (a menos que **SQLSetConnectAttr** y **SQLSetConnectOption** no son compatibles, que es poco probable). Cambiar del modo de confirmación manual al modo de confirmación automática automáticamente confirma cualquier transacción abierta en la conexión.
