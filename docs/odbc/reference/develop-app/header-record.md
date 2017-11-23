---
title: Registro de encabezado | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13bab46b1340d152a6b91919bdadc59e987edde3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="header-record"></a>Registro de encabezado
Los campos en el registro de encabezado contienen información general sobre la ejecución de una función, incluido el código de retorno, el recuento de filas, el número de registros de estado y tipo de instrucción ejecutada. El registro de encabezado siempre se crea, a menos que la función devuelva SQL_INVALID_HANDLE. Para obtener una lista completa de campos en el registro de encabezado, vea el [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descripción de la función.
