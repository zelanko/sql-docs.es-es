---
description: Registro de encabezado
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
ms.openlocfilehash: 4de764381e54a0b3485130c1a3bdf25b2a9bf9fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476647"
---
# <a name="header-record"></a>Registro de encabezado
Los campos del registro de encabezado contienen información general sobre la ejecución de una función, incluidos el código de retorno, el recuento de filas, el número de registros de estado y el tipo de instrucción ejecutada. El registro de encabezado siempre se crea a menos que la función devuelva SQL_INVALID_HANDLE. Para obtener una lista completa de los campos del registro de encabezado, vea la descripción de la función [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) .
