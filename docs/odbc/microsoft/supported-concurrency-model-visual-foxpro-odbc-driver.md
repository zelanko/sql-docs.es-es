---
description: Modelo de simultaneidad compatibles (el controlador ODBC de Visual FoxPro)
title: Modelo de simultaneidad compatible (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be0a7e9ea3700941282f23956a8c304a1ef7f5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500108"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Modelo de simultaneidad compatibles (el controlador ODBC de Visual FoxPro)
El controlador ODBC de Visual FoxPro admite la *simultaneidad de solo lectura*. La aplicación puede llamar a [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con una opción SQL_CONCURRENCY de SQL_CONCUR_READ_ONLY.  
  
 Para obtener más información, vea la [Referencia del programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>simultaneidad de solo lectura  
 No se puede actualizar el cursor.  
  
## <a name="row-versioning"></a>versiones de fila  
 Compatibilidad con la marca de tiempo esencialmente, en la que las versiones de fila se comparan en tiempo de actualización.
