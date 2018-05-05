---
title: Controladores de base de datos de diagnóstico para escritorio | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d5d82eb22f57fd033ea9250e1dd5532e72174e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico de controladores de escritorio de la base de datos
Todos los errores y advertencias no modificado o parcialmente activada por el Administrador de controladores se administran mediante el controlador. El controlador también asigna nativo errores o los errores devueltos por el origen de datos para SQLSTATEs. Cada función aparecen en la *referencia del programador de ODBC* contiene una sección de "Diagnostics" que especifica las condiciones y los mensajes.  
  
 Aplicaciones llaman a **SQLGetDiagRec** para recuperar SQLSTATE, el código de error nativo y mensajes de diagnóstico. Al llamar a **SQLGetDiagField** y especificar el campo recupera todos los campos de diagnóstico individuales. El nivel de compatibilidad de los identificadores de diagnóstico se muestra en la tabla siguiente.  
  
|DiagIdentifiers|Nivel de soporte técnico|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|No compatible|  
|SQL_DIAG_CLASS_ORIGIN|Compatible. Siempre "ODBC 3.0" para las versiones 3.0 y versiones posteriores de este controlador.|  
|SQL_DIAG_COLUMN_NUMBER|Compatible|  
|SQL_DIAG_CURSOR_ROW_COUNT|No compatible|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|No compatible|  
|SQL_DIAG_MESSAGE_TEXT|Compatible|  
|SQL_DIAG_NATIVE|Compatible|  
|SQL_DIAG_NUMBER|Compatible|  
|SQL_DIAG_RETURNCODE|Compatible, pero implementado por el Administrador de controladores|  
|SQL_DIAG_ROW_COUNT|Compatible|  
|SQL_DIAG_ROW_NUMBER|Compatible|  
|SQL_DIAG_SERVER_NAME|No compatible|  
|SQL_DIAG_SQLSTATE|Compatible|  
|SQL_DIAG_SUBCLASS_ORIGIN|Compatible|
