---
title: Comprobaciones de valores de argumento | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a5a57d03f7f1da36115bd0e69c11c33289547f9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="argument-value-checks"></a>Comprobaciones de valores de argumento
El Administrador de controladores comprueba los siguientes tipos de argumentos. A menos que se indique lo contrario, el Administrador de controladores devuelve SQL_ERROR si hay errores en los valores de argumento.  
  
-   Identificadores de entorno, conexión e instrucción normalmente no pueden ser punteros null. El Administrador de controladores devuelve SQL_INVALID_HANDLE cuando encuentra un identificador nulo.  
  
-   Requiere argumentos de puntero, como *OutputHandlePtr* en **SQLAllocHandle** y *CursorName* en **SQLSetCursorName**, no puede ser punteros null.  
  
-   Marcas de opción que no admiten valores específicos del controlador deben ser un valor válido. Por ejemplo, *operación* en **SQLSetPos** debe ser SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE o SQL_ADD.  
  
-   Marcas de opción deben admitirse en la versión de ODBC compatible con el controlador. Por ejemplo, *tipo de información* en **SQLGetInfo** no puede ser SQL_ASYNC_MODE (introducida en ODBC 3.0) cuando se llama a un controlador ODBC 2.0.  
  
-   Números de columna y el parámetro deben ser mayor que 0 o mayor o igual a 0, dependiendo de la función. El controlador debe comprobar el límite superior de estos valores de argumento basándose en el conjunto de resultados actual o la instrucción SQL.  
  
-   Argumentos de longitud/indicador como argumentos de longitud de búfer de datos deben contener los valores adecuados. Por ejemplo, el argumento que especifica la longitud de un nombre de tabla en **SQLColumns** (*NameLength3*) debe ser SQL_NTS o un valor mayor que 0; *BufferLength* en **SQLDescribeCol** debe ser mayor o igual que 0. El controlador también deba comprobar estos argumentos. Por ejemplo, podría comprobar que *NameLength3* es menor o igual que la longitud máxima de un nombre de tabla del origen de datos.

