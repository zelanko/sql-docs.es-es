---
title: La confirmación y el comportamiento de la reversión | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d859dcaad175ce7f340ecbf8ad8e08492d22b63c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="commit-and-rollback-behavior"></a>Confirmación y el comportamiento de reversión
Es un comportamiento común entre servidor DBMS cerrar los cursores y descartar las instrucciones preparadas cuando una instrucción se confirma o revierte. Bases de datos de escritorio son más propensos a mantener cursores abiertos y mantener las instrucciones preparadas. Para obtener más información, vea las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función y [efecto de las transacciones en instrucciones preparadasycursores](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
