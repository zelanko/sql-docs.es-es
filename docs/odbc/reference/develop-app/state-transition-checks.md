---
title: "Comprobaciones de transición de estado | Documentos de Microsoft"
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
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3e69167072663f2fa4e2aea0e13611f5cf15cd8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="state-transition-checks"></a>Comprobaciones de transición de estado
El Administrador de controladores comprueba que el estado del entorno, la conexión o la instrucción es adecuado para la función que se llama. Por ejemplo, una conexión debe estar en una asignación estado cuando **SQLConnect** se denomina; debe ser una instrucción en un preparada estado cuando **SQLExecute** se llama. El Administrador de controladores devuelve SQL_ERROR si hay errores de transición de estado.
