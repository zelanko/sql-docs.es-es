---
title: Asignación de los tipos de información de Cursor Attributes1 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e9549c442e301f3a6ed8d3da9c73d52177adf01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628899"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Asignar los tipos de información de Cursor Attributes1
Cuando un ODBC 3. *x* aplicación llama a **SQLGetInfo** en un 2 de ODBC *.x* controlador con el tipo de información SQL_XXXX_CURSOR_ATTRIBUTES1 (para dinámico, solo avance, de los cursores, o cursores estáticos), la configuración de los bits devueltos por el Administrador de controladores depende de qué el 2 de ODBC. *x* controlador devuelve el 2 de ODBC correspondiente. *x* tipos de información. Los bits se establecen como se muestra en la tabla siguiente.  
  
|Bit en<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Tipo de cursor|ODBC 2. *x* información<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|All|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dinámico, de los cursores, estático|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dinámico, de los cursores, estático|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|All|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dinámico, de los cursores, estático|SQL_POS_OPERATIONS|
