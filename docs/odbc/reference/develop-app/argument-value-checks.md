---
title: Comprobaciones de valores de argumento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 013c8f80a672ed691e7519b318206c406171cfbc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077116"
---
# <a name="argument-value-checks"></a>Comprobaciones de valores de argumento
El Administrador de controladores comprueba los siguientes tipos de argumentos. A menos que se indique lo contrario, el Administrador de controladores devuelve SQL_ERROR si hay errores en los valores de argumento.  
  
-   Normalmente, los identificadores de entorno, la conexión y la instrucción no pueden ser punteros nulos. El Administrador de controladores devuelva SQL_INVALID_HANDLE cuando encuentra un identificador nulo.  
  
-   Necesarios como argumentos de puntero, *OutputHandlePtr* en **SQLAllocHandle** y *CursorName* en **SQLSetCursorName**, no puede ser punteros null.  
  
-   Marcas de opción que no admiten valores específicos del controlador deben ser un valor válido. Por ejemplo, *operación* en **SQLSetPos** debe ser SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE o SQL_ADD.  
  
-   Marcas de opción deben ser compatibles en la versión de ODBC compatible con el controlador. Por ejemplo, *InfoType* en **SQLGetInfo** no puede ser SQL_ASYNC_MODE (introducida en ODBC 3.0) cuando se llama a un controlador ODBC 2.0.  
  
-   Números de columna y el parámetro deben ser mayor que 0 o mayor o igual a 0, dependiendo de la función. El controlador debe comprobar el límite superior de estos valores de argumento basándose en el conjunto de resultados actual o la instrucción SQL.  
  
-   Argumentos de longitud/indicador y argumentos de longitud de búfer de datos deben contener los valores adecuados. Por ejemplo, el argumento que especifica la longitud de un nombre de tabla en **SQLColumns** (*NameLength3*) debe ser SQL_NTS o un valor mayor que 0. *BufferLength* en **SQLDescribeCol** debe ser mayor o igual que 0. También es posible que el controlador comprobar estos argumentos. Por ejemplo, podría comprobar que *NameLength3* es menor o igual que la longitud máxima de un nombre de tabla del origen de datos.
