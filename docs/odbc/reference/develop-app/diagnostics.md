---
description: Diagnóstico
title: Diagnósticos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 918dce41ca1c7e7b43c1a6d25de2c75a83312715
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476717"
---
# <a name="diagnostics"></a>Diagnóstico
Las funciones de ODBC devuelven información de diagnóstico de dos maneras. El código de retorno indica el éxito o error general de la función, mientras que los registros de diagnóstico proporcionan información detallada sobre la función. Al menos un registro de diagnóstico: se devuelve el registro de encabezado, incluso si la función se ejecuta correctamente.  
  
 La información de diagnóstico se usa durante el desarrollo para detectar errores de programación, como identificadores no válidos y errores de sintaxis en instrucciones SQL codificadas de forma rígida. Se utiliza en tiempo de ejecución para detectar errores y advertencias en tiempo de ejecución, como el truncamiento de datos, las infracciones de acceso y los errores de sintaxis en instrucciones SQL escritas por el usuario.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [Registros de diagnóstico](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Uso de SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementar SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Ejemplos de control de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
