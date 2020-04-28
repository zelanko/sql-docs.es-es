---
title: Identificadores de tipo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a274a19eaa0a2fdf98bcaa9ef42406ee8a6b6461
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306436"
---
# <a name="type-identifiers"></a>Identificadores de tipo
Para describir los tipos de datos de SQL y C, ODBC define dos conjuntos de *identificadores de tipo*. Un identificador de tipo describe el tipo de una columna de SQL o un búfer de C. Es un valor **#define** y normalmente se pasa como argumento de función o se devuelve en metadatos.  
  
 Por ejemplo, la siguiente llamada a **SQLBindParameter** enlaza una variable de tipo SQL_DATE_STRUCT a un parámetro de fecha en una instrucción SQL. El identificador de tipo de C SQL_C_TYPE_DATE especifica el tipo de la variable de *fecha* y el identificador de tipo de SQL SQL_TYPE_DATE especifica el tipo del parámetro dinámico.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
