---
title: Tipos de marcador | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06f720d61ae8be7b1a2c98ce2c749a4265e630d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909306"
---
# <a name="bookmark-types"></a>Tipos de marcador
Todos los marcadores en ODBC 3 *.x* son marcadores de longitud variable. Esto permite que una clave principal o un índice único asociado a una tabla que se usará como un marcador. El marcador también puede ser un valor de 32 bits, que se utilizaba en ODBC 2. *x*. Para especificar que se utiliza un marcador con un cursor, una aplicación ODBC 3 *.x* aplicación establece el atributo de instrucción de SQL_ATTR_USE_BOOKMARK en SQL_UB_VARIABLE. Automáticamente se utiliza un marcador de longitud variable.  
  
 Una aplicación puede llamar a **SQLColAttribute** con el *FieldIdentifier* establecido en SQL_DESC_OCTET_LENGTH para obtener la longitud del marcador. Dado que un marcador de longitud variable puede ser un valor de tipo long, una aplicación no debe enlazarse a la columna 0, a menos que se va a utilizar el marcador para muchas de las filas del conjunto de filas.  
  
 Se admiten marcadores de longitud fija únicamente por compatibilidad con versiones anteriores. Si está un ODBC 2. *x* aplicación trabajar con una aplicación ODBC 3 *.x* controlador llama **SQLSetStmtOption** para establecer SQL_USE_BOOKMARKS en SQL_UB_ON, se asigna en el Administrador de controladores para SQL_UB_VARIABLE . Se utiliza un marcador de longitud variable, incluso si se rellenan sólo de 32 bits del mismo. Si un controlador es compatible con marcadores de longitud fija, admitirá marcadores de longitud variable. Si una aplicación ODBC 3 *.x* aplicación trabajar con una API ODBC 2. *x* controlador llama **SQLSetStmtAttr** para establecer SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE, se asigna en el Administrador de controladores a SQL_UB_ON y se utiliza un marcador de longitud fija de 32 bits. El atributo de instrucción de SQL_ATTR_FETCH_BOOKMARK_PTR, a continuación, debe apuntar a un marcador de 32 bits. Si hay más de 32 bits, como cuando se usan las claves principales como marcadores, los marcadores que se utiliza el cursor debe asignar los valores reales con valores de 32 bits. Por ejemplo, podría generar una tabla hash de ellos. Cuando una aplicación ODBC 3 *.x* aplicación trabajar con una API ODBC 2. *x* controlador enlaza un marcador, la longitud del búfer debe ser 4.
