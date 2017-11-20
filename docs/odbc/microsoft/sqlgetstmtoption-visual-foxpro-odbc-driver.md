---
title: SQLGetStmtOption (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 601dd559d7bf13d1a12d032d8431a8c3fe0287d4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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

