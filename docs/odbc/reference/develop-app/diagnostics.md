---
title: "Diagnóstico | Documentos de Microsoft"
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
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efbc34be3dc532b329863a98305952d90adcc9f5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="diagnostics"></a>Diagnósticos
Las funciones de ODBC devuelven información de diagnóstico de dos maneras. El código de retorno indica el éxito o fracaso de la función global mientras que los registros de diagnóstico proporcionan información detallada acerca de la función. Al menos un registro de diagnóstico, el registro de encabezado, se devuelve aunque la función se realiza correctamente.  
  
 Información de diagnóstico se utiliza en tiempo de desarrollo para detectar errores de programación como identificadores no válidos y errores de sintaxis en instrucciones de SQL codificadas de forma rígida. Se utiliza en tiempo de ejecución para detectar errores en tiempo de ejecución y las advertencias, como truncamiento de datos y las infracciones de acceso, errores de sintaxis en instrucciones SQL escritas por el usuario.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [Registros de diagnóstico](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Uso de SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementar SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Ejemplos de control de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
