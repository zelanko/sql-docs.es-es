---
title: Tipos de marcador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9aca006623d9ddb8292147d8a28c93f912fd25d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794020"
---
# <a name="bookmark-types"></a>Tipos de marcador
Todos los marcadores de ODBC *3.x* son marcadores de longitud variable. Esto permite que una clave principal o un índice único asociado a una tabla que se usará como un marcador. El marcador también puede ser un valor de 32 bits, que se utilizaba en ODBC *2.x*. Para especificar que se usa un marcador con un cursor, una ODBC *3.x* aplicación establece el atributo de instrucción SQL_ATTR_USE_BOOKMARK en SQL_UB_VARIABLE. Automáticamente se usa un marcador de longitud variable.  
  
 Una aplicación puede llamar a **SQLColAttribute** con el *FieldIdentifier* establecido en SQL_DESC_OCTET_LENGTH para obtener la longitud del marcador. Dado un marcador de longitud variable puede ser un valor de tipo long, una aplicación no debe enlazar a la columna 0, a menos que se usará el marcador para muchas de las filas del conjunto de filas.  
  
 Marcadores de longitud fija se admiten únicamente por compatibilidad con versiones anteriores. Si un ODBC *2.x* la aplicación funciona con un ODBC *3.x* controlador llama a **SQLSetStmtOption** para establecer SQL_USE_BOOKMARKS SQL_UB_ON, se asigna en el Administrador de controladores a SQL_ UB_VARIABLE. Se utiliza un marcador de longitud variable, incluso si se rellenan sólo de 32 bits del mismo. Si un controlador es compatible con marcadores de longitud fija, lo será compatible con marcadores de longitud variable. Si un ODBC *3.x* la aplicación funciona con un ODBC *2.x* controlador llama a **SQLSetStmtAttr** para establecer SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE, se asigna en el controlador Se usa el administrador para SQL_UB_ON y un marcador de longitud fija de 32 bits. El atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR, a continuación, debe apuntar a un marcador de 32 bits. Si los marcadores que se utilizan son más de 32 bits, por ejemplo, cuando se usan claves principales como marcadores, el cursor debe asignar los valores reales a valores de 32 bits. Por ejemplo, se podría compilar una tabla hash de ellos. Cuando un ODBC *3.x* la aplicación funciona con un ODBC *2.x* controlador enlaza un marcador, la longitud del búfer debe ser 4.
