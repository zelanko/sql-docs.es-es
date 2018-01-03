---
title: Comprobaciones de errores general | Documentos de Microsoft
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
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b224d4df223d189e2532a7ed195ba6bfa9822b4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="general-error-checks"></a>Comprobaciones de errores generales
El Administrador de controladores comprueba un error general. Siempre devuelve SQL_ERROR cuando encuentra el siguiente error: la función debe ser compatibles con el controlador.
