---
title: Diagnóstico para controladores de base de datos de escritorio ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99603c047e77d3cd3e077c1b07c2192eeb65f93c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303486"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico de controladores de escritorio de la base de datos
Todos los errores y advertencias no comprobados o parcialmente comprobados por el Administrador de controladores son controlados por el controlador. El controlador también asigna errores nativos, o errores devueltos por el origen de datos, a SQLSTATEs. Cada función enumerada en la *referencia del programador ODBC* contiene una sección "Diagnostics" que especifica las condiciones y los mensajes.  
  
 Las aplicaciones llaman a **SQLGetDiagRec** para recuperar SQLSTATE, código de error nativo y mensajes de diagnóstico. Llamar a **SQLGetDiagField** y especificar el campo recupera campos de diagnóstico individuales. El nivel de soporte de los identificadores de diagnóstico se muestra en la tabla siguiente.  
  
|DiagIdentifiers|Nivel de compatibilidad|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|No compatible|  
|SQL_DIAG_CLASS_ORIGIN|Compatible. Siempre "ODBC 3.0" para las versiones 3.0 y posteriores de este controlador.|  
|SQL_DIAG_COLUMN_NUMBER|Compatible|  
|SQL_DIAG_CURSOR_ROW_COUNT|No compatible|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|No compatible|  
|SQL_DIAG_MESSAGE_TEXT|Compatible|  
|SQL_DIAG_NATIVE|Compatible|  
|SQL_DIAG_NUMBER|Compatible|  
|SQL_DIAG_RETURNCODE|Apoyado pero implementado por el Administrador de Conductores|  
|SQL_DIAG_ROW_COUNT|Compatible|  
|SQL_DIAG_ROW_NUMBER|Compatible|  
|SQL_DIAG_SERVER_NAME|No compatible|  
|SQL_DIAG_SQLSTATE|Compatible|  
|SQL_DIAG_SUBCLASS_ORIGIN|Compatible|
