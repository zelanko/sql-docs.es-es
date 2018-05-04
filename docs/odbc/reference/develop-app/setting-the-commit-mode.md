---
title: Establecer el modo de confirmación | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3e3abc5cd7648dce484b6347c30d9290b9fc76a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setting-the-commit-mode"></a>Establecer el modo de confirmación
Las aplicaciones especificar el modo de transacción con el atributo de conexión SQL_ATTR_AUTOCOMMIT. De forma predeterminada, las transacciones de ODBC están en modo de confirmación automática (a menos que **SQLSetConnectAttr** y **SQLSetConnectOption** no son compatibles, que es poco probable). Cambiar del modo de confirmación manual al modo de confirmación automática automáticamente confirma cualquier transacción abierta en la conexión.
