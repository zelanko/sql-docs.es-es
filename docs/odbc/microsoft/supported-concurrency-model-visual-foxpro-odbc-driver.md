---
title: Admite el modelo de simultaneidad (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e06adec755df6c412d13fd8c2b892db8977b3a53
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modelo de simultaneidad compatibles (el controlador ODBC de Visual FoxPro)
Es compatible con el controlador ODBC de Visual FoxPro *simultaneidad de solo lectura*. La aplicación puede llamar a [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con una opción SQL_CONCURRENCY de SQL_CONCUR_READ_ONLY.  
  
 Para obtener más información, consulte el [referencia del programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>simultaneidad de solo lectura  
 No se puede actualizar el cursor.  
  
## <a name="row-versioning"></a>versiones de fila  
 Básicamente marca de tiempo soporte técnico, en qué fila se comparan versiones durante la actualización.
