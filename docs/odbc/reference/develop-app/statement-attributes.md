---
title: Atributos de la instrucción ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec24cc43e8c57e47ddda9f20fac1807f42453e84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299648"
---
# <a name="statement-attributes"></a>Atributos de instrucción
Los atributos de instrucción son características de la instrucción. Por ejemplo, si se deben usar marcadores y qué tipo de cursor usar con el conjunto de resultados de la instrucción son atributos de instrucción.  
  
 Los atributos de instrucción se establecen con **SQLSetStmtAttr** y su configuración actual recuperada con **SQLGetStmtAttr**. No hay ningún requisito de que una aplicación establezca atributos de instrucción; todos los atributos de instrucción tienen valores predeterminados, algunos de los cuales son específicos del controlador.  
  
 Cuando se puede establecer un atributo de instrucción depende del propio atributo. Los atributos de SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR y SQL_ATTR_USE_BOOKMARKS instrucción deben establecerse antes de ejecutar la instrucción. Los atributos de instrucción SQL_ATTR_ASYNC_ENABLE y SQL_ATTR_NOSCAN se pueden establecer en cualquier momento, pero no se aplican hasta que se vuelva a utilizar la instrucción. SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS y SQL_ATTR_QUERY_TIMEOUT atributos de instrucción se pueden establecer en cualquier momento, pero es específico del controlador si se aplican antes de que se vuelva a usar la instrucción. Los atributos de instrucción restantes se pueden establecer en cualquier momento.  
  
> [!NOTE]  
>  La capacidad de establecer atributos de instrucción en el nivel de conexión mediante una llamada a **SQLSetConnectAttr** ha quedado en desuso en ODBC 3. *x*. ODBC 3. *x* las aplicaciones nunca deben establecer atributos de instrucción en el nivel de conexión. ODBC 3. *x* los controladores solo necesitan admitir esta funcionalidad si deben trabajar con ODBC 2. *x* aplicaciones. Para obtener más información, vea [Asignación de SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
>   
>  Una excepción a esto es el SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE atributos, que son atributos de conexión y atributos de instrucción y se pueden establecer en el nivel de conexión o en el nivel de instrucción.  
>   
>  Ninguno de los atributos de instrucción introducidos en ODBC 3. *x* (excepto para SQL_ATTR_METADATA_ID) se puede establecer en el nivel de conexión.  
  
 Para obtener más información, vea la descripción de la función [SQLSetStmtAttr.](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)
