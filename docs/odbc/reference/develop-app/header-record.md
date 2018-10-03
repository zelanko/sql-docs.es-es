---
title: Registro de encabezado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7b6ffacb618dd2b7714be59814f3f1a88a52228
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813923"
---
# <a name="header-record"></a>Registro de encabezado
Los campos en el registro de encabezado contienen información general sobre la ejecución de una función, incluido el código de retorno, el recuento de filas, el número de registros de estado y tipo de instrucción ejecutada. El registro de encabezado siempre se crea, a menos que la función devuelva SQL_INVALID_HANDLE. Para obtener una lista completa de campos en el registro de encabezado, vea el [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descripción de la función.
