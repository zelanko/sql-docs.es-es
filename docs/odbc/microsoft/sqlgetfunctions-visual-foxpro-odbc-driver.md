---
title: SQLGetFunctions (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0552f93e5318e5a282b92c88fe12345e6883670d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Devuelve TRUE para todas las funciones compatibles.  
  
 El controlador ODBC de Visual FoxPro admite funciones de todos los núcleos de la API de ODBC y nivel 1. En la tabla siguiente indica si el controlador admite una determinada función de nivel 2.  
  
|*Función*|Admitida|  
|----------------|---------------|  
|SQL_API_SQLBROWSECONNECT|No|  
|SQL_API_SQLCOLUMNPRIVELEGES|No|  
|SQL_API_SQLDATASOURCES|Sí|  
|SQL_API_SQLDESCRIBEPARAM|No|  
|SQL_API_SQLDRIVERS|Sí|  
|SQL_API_SQLEXTENDEDFETCH|Sí|  
|SQL_API_SQLFOREIGNKEYS|No|  
|SQL_API_SQLMORERESULTS|Sí|  
|SQL_API_SQLNATIVESQL|No|  
|SQL_API_SQLNUMPARAMS|Sí|  
|SQL_API_SQLPARAMOPTIONS|Sí|  
|SQL_API_SQLPRIMARYKEYS|Sí|  
|SQL_API_SQLPROCEDURECOLUMNS|No|  
|SQL_API_SQLPROCEDURES|No|  
|SQL_API_SQLSETPOS|Sí|  
|SQL_API_SQLSETSCROLLOPTIONS|Sí|  
|SQL_API_SQLTABLEPRIVILEGES|No|  
  
 Para obtener más información, consulte [SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md) en el *referencia del programador de ODBC*.

