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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077116"
---
# <a name="argument-value-checks"></a>Comprobaciones de valores de argumento
El administrador de controladores comprueba los siguientes tipos de argumentos. A menos que se indique lo contrario, el administrador de controladores devuelve SQL_ERROR para los errores en los valores de argumento.  
  
-   Los identificadores de entorno, conexión y instrucción normalmente no pueden ser punteros nulos. El administrador de controladores devuelve SQL_INVALID_HANDLE cuando encuentra un identificador nulo.  
  
-   Los argumentos de puntero necesarios, como *OutputHandlePtr* en **SQLAllocHandle** y *CursorName* en **SQLSetCursorName**, no pueden ser punteros nulos.  
  
-   Las marcas de opciones que no admiten valores específicos del controlador deben ser un valor válido. Por ejemplo, la *operación* en **SQLSetPos** debe ser SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE o SQL_ADD.  
  
-   Las marcas de opciones deben ser compatibles con la versión de ODBC que admite el controlador. Por ejemplo, *InfoType* en **SQLGetInfo** no se puede SQL_ASYNC_MODE (introducido en ODBC 3,0) cuando se llama a un controlador ODBC 2,0.  
  
-   Los números de columna y parámetro deben ser mayores que 0 o mayor o igual que 0, dependiendo de la función. El controlador debe comprobar el límite superior de estos valores de argumento en función del conjunto de resultados actual o de la instrucción SQL.  
  
-   Los argumentos de longitud/indicador y longitud del búfer de datos deben contener los valores adecuados. Por ejemplo, el argumento que especifica la longitud de un nombre de tabla en **SQLColumns** (*NameLength3*) debe ser SQL_NTS o un valor mayor que 0; *BufferLength* en **SQLDescribeCol** debe ser mayor o igual que 0. Es posible que el controlador también tenga que comprobar estos argumentos. Por ejemplo, podría comprobar que *NameLength3* es menor o igual que la longitud máxima de un nombre de tabla en el origen de datos.
