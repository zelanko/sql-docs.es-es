---
title: Marcadores de parámetros en las llamadas a procedimiento | Documentos de Microsoft
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
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d21de0ce752296e1534b01c197f18934862eec85
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-markers-in-procedure-calls"></a>Marcadores de parámetros en las llamadas a procedimiento
Al llamar a procedimientos que aceptan parámetros, aplicaciones interoperables deben utilizar marcadores de parámetros en lugar de valores de parámetro literal. Algunos orígenes de datos no admiten el uso de valores de parámetro literal en llamadas a procedimiento. Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md). Para obtener más información sobre cómo llamar a procedimientos, consulte [las llamadas a procedimiento](../../../odbc/reference/develop-app/procedure-calls.md), más adelante en esta sección.
