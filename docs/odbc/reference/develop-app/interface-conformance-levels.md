---
title: Niveles de compatibilidad de la interfaz | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0abde908ca3205cc10a35c310b508c5142fcb82c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="interface-conformance-levels"></a>Niveles de compatibilidad de interfaz
El propósito de la redistribución es informar a la aplicación qué características están disponibles a él desde el controlador. Un esquema de redistribución basado en funciones no lo suficientemente lograr este objetivo. En ODBC 3. *x*, los controladores se clasifican en función de las características que poseen. Compatibilidad con la característica puede incluir compatibilidad con la función; También puede incluir la compatibilidad con un campo descriptor, un atributo de instrucción, un valor de "Y" para un tipo de información devolviendo por **SQLGetInfo**, y así sucesivamente.  
  
 Para simplificar la especificación de conformidad de interfaz, ODBC define tres niveles de cumplimiento. Para cumplir con un nivel de conformidad determinado, un controlador debe cumplir todos los requisitos de ese nivel de conformidad. Conformidad con un nivel determinado implica conformidad completa con todos los niveles inferiores.  
  
 Niveles de compatibilidad no siempre dividir claridad en soporte técnico para obtener una lista específica de las funciones ODBC, pero especifican las características admitidas, como se muestra en las secciones siguientes. Para proporcionar compatibilidad para una característica, un controlador debe admitir algunas o todas las formas de las llamadas a determinadas funciones ODBC (para obtener más información, consulte [función conformidad](../../../odbc/reference/develop-app/function-conformance.md)), establecer determinados atributos (vea [conformidad de atributo ](../../../odbc/reference/develop-app/attribute-conformance.md)) y algunos de los campos descriptor (vea [conformidad de campo de Descriptor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 La aplicación detecta el nivel de conformidad con la interfaz del controlador al conectarse a un origen de datos y llamar a **SQLGetInfo** con la opción SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Los controladores son gratuitas implementar características más allá del nivel al que afirman conformidad completa. Las capacidades adicionales para detectar las aplicaciones mediante una llamada a **SQLGetFunctions** (para determinar qué funciones ODBC están presentes) y **SQLGetInfo** (para consultar varias otras funciones ODBC).  
  
 Hay tres niveles de compatibilidad de interfaz ODBC: principal, nivel 1 y nivel 2.  
  
> [!NOTE]  
>  Estos niveles no tienen requisitos diferentes que los niveles de conformidad de la API de ODBC del mismo nombre en ODBC 2*.x*. En concreto, todas las características implícito en ODBC 2*.x* conformidad API nivel 1 ahora forman parte del nivel de conformidad de interfaz de núcleo. Como resultado, es podrán que muchos controladores ODBC informe conformidad de interfaz de nivel de núcleo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Conformidad de interfaz de núcleo](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Cumplimiento de la interfaz de nivel 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformidad de función](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformidad de atributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformidad de campo de descriptor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
