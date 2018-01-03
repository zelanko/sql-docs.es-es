---
title: "Marcadores de parámetros en las llamadas a procedimiento | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 51333ea1f65107ebbd21e5a2f870a974dd8c3a48
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="parameter-markers-in-procedure-calls"></a>Marcadores de parámetros en las llamadas a procedimiento
Al llamar a procedimientos que aceptan parámetros, aplicaciones interoperables deben utilizar marcadores de parámetros en lugar de valores de parámetro literal. Algunos orígenes de datos no admiten el uso de valores de parámetro literal en llamadas a procedimiento. Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md). Para obtener más información sobre cómo llamar a procedimientos, consulte [las llamadas a procedimiento](../../../odbc/reference/develop-app/procedure-calls.md), más adelante en esta sección.
