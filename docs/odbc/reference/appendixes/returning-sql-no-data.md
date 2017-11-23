---
title: Devuelve SQL_NO_DATA | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
ms.openlocfilehash: bf27a50915d9af31eaa280525736cacf7faf06db
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="returning-sqlnodata"></a>Devuelve SQL_NO_DATA
Cuando un ODBC 2. *x* aplicación trabaja con una aplicación ODBC 3*.x* controlador llama **SQLExecDirect**, **SQLExecute**, o **SQLParamData**, y una actualización por búsqueda o una instrucción delete se ejecutó pero no afectó a ninguna fila en el origen de datos ODBC 3*.x* controlador debería devolver SQL_SUCCESS. Cuando una aplicación ODBC 3*.x* aplicación trabajar con una aplicación ODBC 3*.x* controlador llama **SQLExecDirect**, **SQLExecute**, o  **SQLParamData** con el mismo resultado, ODBC 3*.x* controlador debería devolver SQL_NO_DATA.  
  
 Si una búsqueda instrucción update o delete en un lote de instrucciones no afecta a las filas del origen de datos, **SQLMoreResults** devuelve SQL_SUCCESS. No se devolverá SQL_NO_DATA, ya que eso significaría que ya no queden más resultados, no que es el resultado de una actualización/eliminación delete por búsqueda que no hay filas afectadas.
