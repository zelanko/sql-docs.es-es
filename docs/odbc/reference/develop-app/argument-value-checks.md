---
title: Comprobaciones del valor de los argumentos ( Argument Value Checks) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c6e4de16c4a1a80be893acbc7a1993b375f2fee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298832"
---
# <a name="argument-value-checks"></a>Comprobaciones de valores de argumento
El Administrador de controladores comprueba los siguientes tipos de argumentos. A menos que se indique lo contrario, el Administrador de controladores devuelve SQL_ERROR de errores en los valores de argumento.  
  
-   Los identificadores de entorno, conexión e instrucción normalmente no pueden ser punteros nulos. El Administrador de controladores devuelve SQL_INVALID_HANDLE cuando encuentra un identificador nulo.  
  
-   Argumentos de puntero necesarios, como *OutputHandlePtr* en **SQLAllocHandle** y *CursorName* en **SQLSetCursorName**, no pueden ser punteros nulos.  
  
-   Las marcas de opción que no admiten valores específicos del controlador deben ser un valor legal. Por ejemplo, *Operation* en **SQLSetPos** debe ser SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE o SQL_ADD.  
  
-   Los indicadores de opción deben admitirse en la versión de ODBC admitida por el controlador. Por ejemplo, *InfoType* en **SQLGetInfo** no se puede SQL_ASYNC_MODE (introducido en ODBC 3.0) al llamar a un controlador ODBC 2.0.  
  
-   Los números de columna y parámetro deben ser mayores que 0 o mayores o iguales que 0, dependiendo de la función. El controlador debe comprobar el límite superior de estos valores de argumento en función del conjunto de resultados actual o la instrucción SQL.  
  
-   Los argumentos de longitud/indicador y los argumentos de longitud del búfer de datos deben contener valores adecuados. Por ejemplo, el argumento que especifica la longitud de un nombre de tabla en **SQLColumns** (*NameLength3*) debe ser SQL_NTS o un valor mayor que 0; *BufferLength* en **SQLDescribeCol** debe ser mayor o igual que 0. Es posible que el controlador también deba comprobar estos argumentos. Por ejemplo, podría comprobar que *NameLength3* es menor o igual que la longitud máxima de un nombre de tabla en el origen de datos.
