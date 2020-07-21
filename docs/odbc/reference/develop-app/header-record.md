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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372185966cc1644147feb2683177ae3a5b69e788
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300185"
---
# <a name="header-record"></a>Registro de encabezado
Los campos del registro de encabezado contienen información general sobre la ejecución de una función, incluidos el código de retorno, el recuento de filas, el número de registros de estado y el tipo de instrucción ejecutada. El registro de encabezado siempre se crea a menos que la función devuelva SQL_INVALID_HANDLE. Para obtener una lista completa de los campos del registro de encabezado, vea la descripción de la función [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) .
