---
title: Funciones del sistema | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0c7817d37e14ad07b9cc64f59691c27cf665177
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070093"
---
# <a name="system-functions"></a>Funciones del sistema
En la tabla siguiente se enumeran las funciones del sistema que se incluyen en el conjunto de funciones escalares de ODBC. Al llamar a **SQLGetInfo** con un *tipo de información* de SQL_SYSTEM_FUNCTIONS, una aplicación puede determinar qué funciones del sistema son compatibles con un controlador.  
  
 Los argumentos indicados como *exp* pueden ser el nombre de una columna, el resultado de otra función escalar o un literal, donde el tipo de datos subyacente podría representarse como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP.  
  
 Los argumentos indicados como *valor* pueden ser una constante literal, donde el tipo de datos subyacente se puede representar como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP.  
  
 Los valores devueltos se representan como tipos de datos ODBC.  
  
|Función|Descripción|  
|--------------|-----------------|  
|**Base de datos ()** (ODBC 1,0)|Devuelve el nombre de la base de datos correspondiente al identificador de conexión. (El nombre de la base de datos también está disponible llamando a **SQLGetConnectOption** con la opción de conexión SQL_CURRENT_QUALIFIER).|  
|**IFNULL (** _exp_,_Value_**)** (ODBC 1,0)|Si *exp* es null, se devuelve *Value* . Si *exp* no es null, se devuelve *exp* . El tipo de datos o los tipos de *valor* posibles deben ser compatibles con el tipo de datos de *exp*.|  
|**User ()** (ODBC 1,0)|Devuelve el nombre de usuario en el DBMS. (El nombre de usuario también está disponible por medio de **SQLGetInfo** especificando el tipo de información: SQL_USER_NAME). Puede ser diferente del nombre de inicio de sesión.|
