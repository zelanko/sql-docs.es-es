---
description: Atributos de instrucción
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e2106a952bfdd7945d5d11ddde39138d0c82a14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476357"
---
# <a name="statement-attributes"></a>Atributos de instrucción
Los atributos de instrucción son características de la instrucción. Por ejemplo, si se usan marcadores y el tipo de cursor que se va a usar con el conjunto de resultados de la instrucción son atributos de instrucción.  
  
 Los atributos de instrucción se establecen con **SQLSetStmtAttr** y su configuración actual se recupera con **SQLGetStmtAttr**. No es necesario que una aplicación establezca atributos de instrucción; todos los atributos de instrucción tienen valores predeterminados, algunos de los cuales son específicos del controlador.  
  
 Cuando se puede establecer un atributo de instrucción depende del propio atributo. Los atributos de instrucción SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR y SQL_ATTR_USE_BOOKMARKS se deben establecer antes de que se ejecute la instrucción. Los atributos de instrucción SQL_ATTR_ASYNC_ENABLE y SQL_ATTR_NOSCAN se pueden establecer en cualquier momento, pero no se aplican hasta que se vuelva a usar la instrucción. Los atributos de instrucción SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS y SQL_ATTR_QUERY_TIMEOUT se pueden establecer en cualquier momento, pero es específico del controlador si se aplican antes de que se vuelva a usar la instrucción. Los atributos restantes de la instrucción se pueden establecer en cualquier momento.  
  
> [!NOTE]  
>  La capacidad de establecer atributos de instrucción en el nivel de conexión llamando a **SQLSetConnectAttr** está en desuso en ODBC 3. *x*. ODBC 3. las aplicaciones *x* nunca deben establecer atributos de instrucción en el nivel de conexión. ODBC 3. los controladores *x* solo necesitan admitir esta funcionalidad si deben funcionar con ODBC 2. aplicaciones *x* . Para obtener más información, consulte [asignación de SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) en el Apéndice G: instrucciones del controlador para la compatibilidad con versiones anteriores.  
>   
>  Una excepción a esto son los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son los atributos de conexión y de instrucción, y se pueden establecer en el nivel de conexión o en el nivel de instrucción.  
>   
>  Ninguno de los atributos de instrucción introducidos en ODBC 3. *x* (excepto para SQL_ATTR_METADATA_ID) se puede establecer en el nivel de conexión.  
  
 Para obtener más información, vea la descripción de la función [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) .
