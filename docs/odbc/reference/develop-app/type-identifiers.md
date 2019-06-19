---
title: Escriba los identificadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbefab0f02f3229d8b4c0a62a568634ec222290b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305669"
---
# <a name="type-identifiers"></a>Identificadores de tipo
Para describir los tipos de datos SQL y C, ODBC define dos conjuntos de *identificadores de tipo*. Un identificador de tipo describe el tipo de un búfer de C o una columna SQL. Es un **#define** valor y se pasa como un argumento de función o devuelto en los metadatos con carácter general.  
  
 Por ejemplo, la siguiente llamada a **SQLBindParameter** enlaza una variable de tipo SQL_DATE_STRUCT a un parámetro de fecha en una instrucción SQL. El identificador de tipo C SQL_C_TYPE_DATE especifica el tipo de la *fecha* variable y el identificador del tipo SQL_TYPE_DATE SQL especifica el tipo del parámetro dinámico.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
