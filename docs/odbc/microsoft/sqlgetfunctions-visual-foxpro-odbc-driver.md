---
title: SQLGetFunctions (controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af7ad2368847ff271dcf81759d6fa06b8a79fb0a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298615"
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: Nivel 1  
  
 Devuelve TRUE para todas las funciones admitidas.  
  
 El controlador ODBC de Visual FoxPro admite todas las funciones ODBC API Core y Level 1. La tabla siguiente indica si el controlador admite una función de nivel 2 específica.  
  
|*Función*|Compatible|  
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
  
 Para obtener más información, vea [SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md) en la *referencia del programador ODBC*.
