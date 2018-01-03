---
title: Usar identificadores de tipo de datos | Documentos de Microsoft
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
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0831a683cca3814712697ebbafffcfcdd1f3f86d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="using-data-type-identifiers"></a>Usar identificadores de tipo de datos
Las aplicaciones utilizan identificadores de tipo de datos de dos maneras: para describir los búferes del controlador y para recuperar metadatos sobre el conjunto de resultados desde el controlador para que pueda determinar qué tipo de C almacena en búfer para utilizar para almacenar los datos. Las aplicaciones llaman a las funciones siguientes para llevar a cabo estas tareas:  
  
-   **SQLBindParameter**, **SQLBindCol**, y **SQLGetData** : para describir el tipo de datos C de búferes de la aplicación.  
  
-   **SQLBindParameter** : para describir el tipo de datos SQL de parámetros dinámicos.  
  
-   **SQLColAttribute** y **SQLDescribeCol** : para recuperar los tipos de datos SQL de columnas del conjunto de resultados.  
  
-   **SQLDescribeParameter** : para recuperar los tipos de datos SQL de parámetros.  
  
-   **SQLColumns**, **SQLProcedureColumns**, y **SQLSpecialColumns** : para recuperar los tipos de datos SQL de diversa información de esquema  
  
-   **SQLGetTypeInfo** : recuperar una lista de tipos de datos admitidos  
  
 Identificadores de tipo de datos se almacenan en el campo SQL_DESC_CONCISE_TYPE de un descriptor. Las funciones de descriptor **SQLSetDescField** y **SQLSetDescRec** puede usarse con los tipos adecuados para realizar las tareas que figuran en la lista anterior. Para obtener más información, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).
