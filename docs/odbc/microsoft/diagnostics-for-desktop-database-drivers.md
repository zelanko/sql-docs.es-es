---
title: Diagnósticos para controladores de base de datos de escritorio | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4e7c8ea96708886f9edf54047bd2a2104ba0ec8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031222"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico de controladores de escritorio de la base de datos
El controlador controla todos los errores y advertencias que no se comprueban o que el administrador de controladores comprueba parcialmente. El controlador también asigna errores nativos o errores devueltos por el origen de datos a SQLSTATEs. Cada una de las funciones enumeradas en la *Referencia del programador de ODBC* contiene una sección de "diagnósticos" que especifica las condiciones y los mensajes.  
  
 Las aplicaciones llaman a **SQLGetDiagRec** para recuperar SQLSTATE, el código de error nativo y los mensajes de diagnóstico. Al llamar a **SQLGetDiagField** y especificar el campo, se recuperan los campos de diagnóstico individuales. El nivel de compatibilidad de los identificadores de diagnóstico se muestra en la tabla siguiente.  
  
|DiagIdentifiers|Nivel de compatibilidad|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|No compatible|  
|SQL_DIAG_CLASS_ORIGIN| Se admite. Siempre es "ODBC 3,0" para las versiones 3,0 y posteriores de este controlador.|  
|SQL_DIAG_COLUMN_NUMBER|Compatible|  
|SQL_DIAG_CURSOR_ROW_COUNT|No compatible|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|No compatible|  
|SQL_DIAG_MESSAGE_TEXT|Compatible|  
|SQL_DIAG_NATIVE|Compatible|  
|SQL_DIAG_NUMBER|Compatible|  
|SQL_DIAG_RETURNCODE|Compatible pero implementado por el administrador de controladores|  
|SQL_DIAG_ROW_COUNT|Compatible|  
|SQL_DIAG_ROW_NUMBER|Compatible|  
|SQL_DIAG_SERVER_NAME|No compatible|  
|SQL_DIAG_SQLSTATE|Compatible|  
|SQL_DIAG_SUBCLASS_ORIGIN|Compatible|
