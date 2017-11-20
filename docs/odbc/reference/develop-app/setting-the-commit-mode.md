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
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d0c38d70b859b1fb986ebaa366a5396159a95da
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-commit-mode"></a>Establecer el modo de confirmación
Las aplicaciones especificar el modo de transacción con el atributo de conexión SQL_ATTR_AUTOCOMMIT. De forma predeterminada, las transacciones de ODBC están en modo de confirmación automática (a menos que **SQLSetConnectAttr** y **SQLSetConnectOption** no son compatibles, que es poco probable). Cambiar del modo de confirmación manual al modo de confirmación automática automáticamente confirma cualquier transacción abierta en la conexión.

