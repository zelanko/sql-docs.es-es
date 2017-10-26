---
title: "Asignar los tipos de información de Cursor Attributes1 | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d8f72fb4246f2ccfded98e63b701b57d3229068
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Asignar los tipos de información de Cursor Attributes1
Cuando un ODBC 3. *x* aplicación llama **SQLGetInfo** en una API ODBC 2*.x* controlador con el tipo de información SQL_XXXX_CURSOR_ATTRIBUTES1 (dinámico, solo avance, keyset-controlador de, o los cursores estáticos), la configuración de los bits devueltos por el Administrador de controladores depende de qué la API ODBC 2. *x* controlador devuelve el 2 de ODBC correspondiente.* x* tipos de información. Los bits se establecen como se muestra en la tabla siguiente.  
  
|Valor del bit en<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Tipo de cursor|ODBC 2. *x* información<br /><br /> Tipo|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|Todos|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dinámicos, cursores-controlados, estático|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dinámicos, cursores-controlados, estático|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|Todos|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dinámicos, cursores-controlados, estático|SQL_POS_OPERATIONS|

