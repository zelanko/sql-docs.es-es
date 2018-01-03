---
title: SQLGetStmtOption (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
helpviewer_keywords: SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9042a1a951d08c60e8dc795cd58f2a525cf39cda
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: Uno nivel  
  
 Devuelve el valor actual de una opción de instrucción.  
  
|*FOption*|Devuelve|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|valor entero de 32 bits que es el marcador para el número de registro actual|  
|SQL_ROW_NUMBER|entero de 32 bits que especifica la posición de la fila actual en el resultado establecido|  
|SQL_TRANSLATE_DLL|Error: "el controlador no capaz."|  
  
 El controlador ODBC de Visual FoxPro no tiene ninguna traducción de archivos DLL.  
  
 Para obtener más información, consulte [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) en el *referencia del programador de ODBC*.
