---
title: Atributos de instrucción | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c74f1a79ef79b682bc2900d671e07bbe34c4dbf5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107275"
---
# <a name="statement-attributes"></a>Atributos de instrucción
Atributos de instrucción son características de la instrucción. Por ejemplo, si usar marcadores y qué tipo de cursor para usar con el resultado de la instrucción establece son atributos de instrucción.  
  
 Atributos de instrucción se establecen con **SQLSetStmtAttr** y su configuración actual se recupera con **SQLGetStmtAttr**. No hay ningún requisito que una aplicación establezca atributos de instrucción; todos los atributos de instrucción tienen valores predeterminados, algunos de los cuales son específicos del controlador.  
  
 Cuando se puede establecer un atributo de instrucción depende el propio atributo. Los atributos de instrucción SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_CURSOR_TYPE y SQL_ATTR_CONCURRENCY deben establecerse antes de que se ejecuta la instrucción. Los atributos de instrucción SQL_ATTR_ASYNC_ENABLE y SQL_ATTR_NOSCAN se pueden establecer en cualquier momento, pero no se aplican hasta que se utiliza la instrucción de nuevo. Atributos de instrucción SQL_ATTR_QUERY_TIMEOUT, SQL_ATTR_MAX_LENGTH y SQL_ATTR_MAX_ROWS se pueden establecer en cualquier momento, pero es específico del controlador si se aplican antes de que se utiliza la instrucción de nuevo. Los demás atributos de instrucción se pueden establecer en cualquier momento.  
  
> [!NOTE]  
>  La capacidad de establecer los atributos de instrucción en el nivel de conexión mediante una llamada a **SQLSetConnectAttr** ha quedado obsoleto en ODBC 3. *x*. ODBC 3. *x* aplicaciones nunca deben establecer los atributos de instrucción en el nivel de conexión. ODBC 3. *x* controladores sólo necesitan admitir esta funcionalidad si trabajan con ODBC 2. *x* aplicaciones. Para obtener más información, consulte [asignación de SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
>   
>  Una excepción a esto es que los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son los atributos de conexión y los atributos de instrucción y se pueden establecer en el nivel de conexión o el nivel de instrucción.  
>   
>  Ninguno de los atributos de instrucción que se introdujo en ODBC 3. *x* (excepto SQL_ATTR_METADATA_ID) se pueden establecer en el nivel de conexión.  
  
 Para obtener más información, consulte el [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descripción de la función.
