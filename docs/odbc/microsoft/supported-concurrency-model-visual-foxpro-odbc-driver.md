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
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f3348850a76bb831c236fd1c1ee49fb89b97504
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modelo de simultaneidad compatibles (el controlador ODBC de Visual FoxPro)
Es compatible con el controlador ODBC de Visual FoxPro *simultaneidad de solo lectura*. La aplicación puede llamar a [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con una opción SQL_CONCURRENCY de SQL_CONCUR_READ_ONLY.  
  
 Para obtener más información, consulte el [referencia del programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>simultaneidad de solo lectura  
 No se puede actualizar el cursor.  
  
## <a name="row-versioning"></a>versiones de fila  
 Básicamente marca de tiempo soporte técnico, en qué fila se comparan versiones durante la actualización.

