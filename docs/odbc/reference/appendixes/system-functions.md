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
manager: craigg
ms.openlocfilehash: 5870cb445d7afd098aba32ffd9be7a88c048bae5
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591519"
---
# <a name="system-functions"></a>Funciones del sistema
En la tabla siguiente se enumera las funciones del sistema que se incluyen en el conjunto de funciones escalares de ODBC. Mediante una llamada a **SQLGetInfo** con un *tipo de información* de SQL_SYSTEM_FUNCTIONS, una aplicación puede determinar qué funciones del sistema son compatibles con un controlador.  
  
 Argumentos que se indican como *exp* puede ser el nombre de una columna, el resultado de otra función escalar o un literal, donde el tipo de datos subyacente podría representarse como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL _BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP.  
  
 Argumentos que se indican como *valor* puede ser una constante literal, donde el tipo de datos subyacente puede representarse como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_ TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP.  
  
 Los valores devueltos se representan como tipos de datos ODBC.  
  
|Función|Descripción|  
|--------------|-----------------|  
|**() DE LA BASE DE DATOS** (ODBC 1.0)|Devuelve el nombre de la base de datos correspondiente al identificador de conexión. (El nombre de la base de datos también está disponible mediante una llamada a **SQLGetConnectOption** con la opción de conexión SQL_CURRENT_QUALIFIER.)|  
|**IFNULL (** _exp_,_valor_**)** (ODBC 1.0)|Si *exp* es null, *valor* se devuelve. Si *exp* no es null, *exp* se devuelve. El tipo de datos o tipos de *valor* debe ser compatible con el tipo de datos de *exp*.|  
|**USUARIO ()** (ODBC 1.0)|Devuelve el nombre de usuario en el DBMS. (El nombre de usuario también está disponible por medio de **SQLGetInfo** especificando el tipo de información: SQL_USER_NAME.) Esto puede ser diferente del nombre de inicio de sesión.|
