---
title: Tipos de cambios | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3db03bfda3e464ebc422cbbc009c586e83863b6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="types-of-changes"></a>Tipos de cambios
Tres tipos de cambios se realizan en ODBC 3. *x* (y cualquier versión de ODBC). Cada una de ellas afecta a la compatibilidad con versiones anteriores de forma diferente y se controla de forma diferente. Estos cambios se describen en la tabla siguiente.  
  
|Tipo de cambio|Description|  
|--------------------|-----------------|  
|Nuevas características|Se trata de características que son nuevas en ODBC 3. *x*, como enlace fuera de línea o descriptores. Estos elementos se implementan solo cuando la aplicación y controlador, así como el Administrador de controladores, son de la versión 3*.x*, por lo que no hay ningún intento para realizar estas compatible con versiones anteriores.|  
|Características duplicados|Se trata de características que existen en ODBC 2*.x* mientras que ODBC 3. *x* pero se implementan de maneras diferentes en cada uno de ellos. Las funciones **SQLAllocHandle** y **SQLAllocStmt** son un ejemplo. Problemas de compatibilidad con versiones anteriores para estas y otras características duplicados principalmente se controlan mediante asignaciones en el Administrador de controladores.|  
|Cambios de comportamiento|Se trata de características que se tratan de forma diferente en ODBC 2*.x* mientras que ODBC 3. *x*. Un valor datetime **#define** es un ejemplo. Estas características se controlan mediante ODBC 3. *x* controlador según un valor de atributo de entorno. (Consulte [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md) para obtener más información.)|
