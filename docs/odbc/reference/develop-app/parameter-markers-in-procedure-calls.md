---
title: Marcadores de parámetros en las llamadas a procedimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00aa87461c1b4a82fbedc7bd7faf1da6ff327265
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199146"
---
# <a name="parameter-markers-in-procedure-calls"></a>Marcadores de parámetros en las llamadas a procedimiento
Al llamar a procedimientos que aceptan parámetros, aplicaciones interoperables deben usar marcadores de parámetros en lugar de los valores de parámetro literal. Algunos orígenes de datos no admite el uso de valores de parámetro literal en llamadas a procedimiento. Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md). Para obtener más información sobre cómo llamar a procedimientos, consulte [las llamadas a procedimiento](../../../odbc/reference/develop-app/procedure-calls.md), más adelante en esta sección.
