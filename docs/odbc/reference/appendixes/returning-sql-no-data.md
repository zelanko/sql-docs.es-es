---
title: Devuelve SQL_NO_DATA | Documentos de Microsoft
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
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 259ec0c9904501069036bdcadcbdad9d0a528d70
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="returning-sqlnodata"></a>Devuelve SQL_NO_DATA
Cuando un ODBC 2. *x* aplicación trabaja con una aplicación ODBC 3*.x* controlador llama **SQLExecDirect**, **SQLExecute**, o **SQLParamData**, y una actualización por búsqueda o una instrucción delete se ejecutó pero no afectó a ninguna fila en el origen de datos ODBC 3*.x* controlador debería devolver SQL_SUCCESS. Cuando una aplicación ODBC 3*.x* aplicación trabajar con una aplicación ODBC 3*.x* controlador llama **SQLExecDirect**, **SQLExecute**, o  **SQLParamData** con el mismo resultado, ODBC 3*.x* controlador debería devolver SQL_NO_DATA.  
  
 Si una búsqueda instrucción update o delete en un lote de instrucciones no afecta a las filas del origen de datos, **SQLMoreResults** devuelve SQL_SUCCESS. No se devolverá SQL_NO_DATA, ya que eso significaría que ya no queden más resultados, no que es el resultado de una actualización/eliminación delete por búsqueda que no hay filas afectadas.
