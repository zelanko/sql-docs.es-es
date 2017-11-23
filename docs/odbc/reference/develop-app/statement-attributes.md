---
title: "Atributos de instrucción | Documentos de Microsoft"
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
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36cc6b00223185a5a1e21708109842384c6ecb1e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="statement-attributes"></a>Atributos de instrucción
Los atributos de instrucción son características de la instrucción. Por ejemplo, si ha establecido para usar marcadores y qué tipo de cursor va a utilizar con el resultado de la instrucción son atributos de instrucción.  
  
 Atributos de instrucción se establecen con **SQLSetStmtAttr** y su configuración actual se recupera con **SQLGetStmtAttr**. No hay ningún requisito que una aplicación establezca atributos de instrucción; todos los atributos de instrucción tienen valores predeterminados, algunos de los cuales son específicos del controlador.  
  
 Cuando se puede establecer un atributo de instrucción depende en el propio atributo. Los atributos de instrucción SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR y SQL_ATTR_USE_BOOKMARKS deben establecerse antes de que se ejecuta la instrucción. Los atributos de instrucción SQL_ATTR_ASYNC_ENABLE y SQL_ATTR_NOSCAN se pueden establecer en cualquier momento, pero no se aplican hasta que se vuelve a usar la instrucción. Atributos de instrucción SQL_ATTR_MAX_LENGTH y SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT se pueden establecer en cualquier momento, pero es específico del controlador si se aplican antes de que se vuelve a usar la instrucción. El resto de atributos de instrucción puede establecerse en cualquier momento.  
  
> [!NOTE]  
>  Permite establecer atributos de instrucción en el nivel de conexión mediante una llamada a **SQLSetConnectAttr** está en desuso en ODBC 3. *x*. ODBC 3. *x* aplicaciones nunca deben establecer los atributos de instrucción en el nivel de conexión. ODBC 3. *x* controladores sólo necesitan admitir esta funcionalidad si deben trabajar con ODBC 2. *x* aplicaciones. Para obtener más información, consulte [SQLSetConnectOption asignación](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.  
>   
>  Una excepción a esto es que los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son atributos de conexión y los atributos de instrucción y se pueden establecer en el nivel de conexión o el nivel de instrucción.  
>   
>  Ninguno de los atributos de instrucción que se introdujo en ODBC 3. *x* (excepto SQL_ATTR_METADATA_ID) se pueden establecer en el nivel de conexión.  
  
 Para obtener más información, consulte el [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descripción de la función.
