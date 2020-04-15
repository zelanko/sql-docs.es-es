---
title: Ajuste del modo de confirmación ( Commit Mode) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299825"
---
# <a name="setting-the-commit-mode"></a>Establecer el modo de confirmación
Las aplicaciones especifican el modo de transacción con el atributo de conexión SQL_ATTR_AUTOCOMMIT. De forma predeterminada, las transacciones ODBC están en modo de confirmación automática (a menos que NO se admitan **SQLSetConnectAttr** y **SQLSetConnectOption,** lo que es poco probable). Al cambiar del modo de confirmación manual al modo de confirmación automática, se confirma automáticamente cualquier transacción abierta en la conexión.
