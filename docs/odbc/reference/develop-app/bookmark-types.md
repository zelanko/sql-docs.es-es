---
description: Tipos de marcador
title: Tipos de marcadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e85d50a5fe3c21707a78ac2572d8a96166745319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476817"
---
# <a name="bookmark-types"></a>Tipos de marcador
Todos los marcadores de ODBC *3. x* son marcadores de longitud variable. Esto permite usar una clave principal o un índice único asociado a una tabla como marcador. El marcador también puede ser un valor de 32 bits, como se usó en ODBC *2. x*. Para especificar que un marcador se utiliza con un cursor, una aplicación ODBC *3. x* establece el atributo de instrucción SQL_ATTR_USE_BOOKMARK en SQL_UB_VARIABLE. Se usa automáticamente un marcador de longitud variable.  
  
 Una aplicación puede llamar a **SQLColAttribute** con el argumento *FieldIdentifier* establecido en SQL_DESC_OCTET_LENGTH para obtener la longitud del marcador. Dado que un marcador de longitud variable puede ser un valor Long, una aplicación no debe enlazarse a la columna 0 a menos que vaya a usar el marcador para muchas de las filas del conjunto de filas.  
  
 Los marcadores de longitud fija solo se admiten para la compatibilidad con versiones anteriores. Si una aplicación ODBC *2. x* que trabaja con un controlador ODBC *3. x* llama a **SQLSetStmtOption** para establecer SQL_USE_BOOKMARKS en SQL_UB_ON, se asigna en el administrador de controladores para SQL_UB_VARIABLE. Se utiliza un marcador de longitud variable, incluso si solo se rellenan 32 bits. Si un controlador admite marcadores de longitud fija, será compatible con marcadores de longitud variable. Si una aplicación ODBC *3. x* que trabaja con un controlador ODBC *2. x* llama a **SQLSetStmtAttr** para establecer SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE, se asigna en el administrador de controladores a SQL_UB_ON y se utiliza un marcador de longitud fija de 32 bits. El atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR debe apuntar a un marcador de 32 bits. Si los marcadores utilizados tienen más de 32 bits, como cuando se usan claves principales como marcadores, el cursor debe asignar los valores reales a valores de 32 bits. Por ejemplo, podría crear una tabla hash de ellos. Cuando una aplicación ODBC *3. x* que trabaja con un controlador ODBC *2. x* enlaza un marcador, la longitud del búfer debe ser 4.
