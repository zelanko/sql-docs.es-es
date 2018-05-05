---
title: SQLGetFunctions (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc3350e8b6a7a4ddcf505fed14a056422cbbbe41
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Devuelve TRUE para todas las funciones compatibles.  
  
 El controlador ODBC de Visual FoxPro admite funciones de todos los núcleos de la API de ODBC y nivel 1. En la tabla siguiente indica si el controlador admite una determinada función de nivel 2.  
  
|*Función*|Compatible|  
|----------------|---------------|  
|SQL_API_SQLBROWSECONNECT|no|  
|SQL_API_SQLCOLUMNPRIVELEGES|no|  
|SQL_API_SQLDATASOURCES|Sí|  
|SQL_API_SQLDESCRIBEPARAM|no|  
|SQL_API_SQLDRIVERS|Sí|  
|SQL_API_SQLEXTENDEDFETCH|Sí|  
|SQL_API_SQLFOREIGNKEYS|no|  
|SQL_API_SQLMORERESULTS|Sí|  
|SQL_API_SQLNATIVESQL|no|  
|SQL_API_SQLNUMPARAMS|Sí|  
|SQL_API_SQLPARAMOPTIONS|Sí|  
|SQL_API_SQLPRIMARYKEYS|Sí|  
|SQL_API_SQLPROCEDURECOLUMNS|no|  
|SQL_API_SQLPROCEDURES|no|  
|SQL_API_SQLSETPOS|Sí|  
|SQL_API_SQLSETSCROLLOPTIONS|Sí|  
|SQL_API_SQLTABLEPRIVILEGES|no|  
  
 Para obtener más información, consulte [SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md) en el *referencia del programador de ODBC*.
