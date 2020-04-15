---
title: Uso de identificadores de tipo de datos ( Data Type Identifiers) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8be8eef0441d48ed03ea6ccf8f656627c1dd9b63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301426"
---
# <a name="using-data-type-identifiers"></a>Usar identificadores de tipo de datos
Las aplicaciones usan identificadores de tipo de datos de dos maneras: para describir sus búferes en el controlador y para recuperar metadatos sobre el conjunto de resultados del controlador para que puedan determinar qué tipo de búferes de C se van a usar para almacenar los datos. Las aplicaciones llaman a las siguientes funciones para realizar estas tareas:  
  
-   **SQLBindParameter**, **SQLBindCol**y **SQLGetData** - para describir el tipo de datos C de los búferes de aplicación.  
  
-   **SQLBindParameter** - para describir el tipo de datos SQL de parámetros dinámicos.  
  
-   **SQLColAttribute** y **SQLDescribeCol:** para recuperar los tipos de datos SQL de las columnas del conjunto de resultados.  
  
-   **SQLDescribeParameter** - para recuperar los tipos de datos SQL de parámetros.  
  
-   **SQLColumns**, **SQLProcedureColumns**y **SQLSpecialColumns** - para recuperar los tipos de datos SQL de varias informaciones de esquema  
  
-   **SQLGetTypeInfo** - para recuperar una lista de tipos de datos admitidos  
  
 Los identificadores de tipo de datos se almacenan en el campo SQL_DESC_CONCISE_TYPE de un descriptor. Las funciones descriptoras **SQLSetDescField** y **SQLSetDescRec** se pueden utilizar con los tipos adecuados para realizar las tareas enumeradas en la lista anterior. Para obtener más información, vea [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).
