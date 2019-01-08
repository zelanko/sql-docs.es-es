---
title: Niveles de compatibilidad de la interfaz | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74d4ceb4532ee09004f035958860833aef488aaa
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206214"
---
# <a name="interface-conformance-levels"></a>Niveles de compatibilidad de interfaz
El propósito de la redistribución es informar a la aplicación qué características están disponibles a él desde el controlador. Un esquema de nivelación de basadas en funciones no lo suficientemente lograr este objetivo. En ODBC 3. *x*, los controladores se clasifican según las características que poseen. Compatibilidad con la característica puede incluir compatibilidad con la función; También puede incluir compatibilidad con un campo descriptor, un atributo de instrucción, un valor "Y" para un tipo de información devolviendo por **SQLGetInfo**, y así sucesivamente.  
  
 Para simplificar la especificación de conformidad de interfaz, ODBC define tres niveles de compatibilidad. Para cumplir con un nivel de conformidad determinado, un controlador debe cumplir todos los requisitos de ese nivel de conformidad. Conformidad con un nivel determinado implica conformidad completa con todos los niveles inferiores.  
  
 Niveles de compatibilidad no siempre dividen perfectamente en soporte técnico para obtener una lista específica de las funciones ODBC, pero especifican las características admitidas, como se muestra en las secciones siguientes. Para proporcionar soporte técnico para una característica, un controlador debe admitir algunos o todos los formularios de las llamadas a determinadas funciones ODBC (para obtener más información, consulte [conformidad de función](../../../odbc/reference/develop-app/function-conformance.md)), establecer determinados atributos (consulte [conformidad de atributo ](../../../odbc/reference/develop-app/attribute-conformance.md)) y algunos de los campos descriptor (consulte [conformidad de campo Descriptor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 La aplicación detecta el nivel de conformidad con la interfaz de un controlador mediante la conexión a un origen de datos y llamar a **SQLGetInfo** con la opción SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Los controladores son gratis implementar características más allá del nivel al que dicen conformidad completa. Las aplicaciones detección cualquier estas capacidades adicionales mediante una llamada a **SQLGetFunctions** (para determinar qué funciones ODBC están presentes) y **SQLGetInfo** (para consultar varias otras funciones de ODBC).  
  
 Hay tres niveles de compatibilidad de interfaz ODBC: Core, nivel 1 y nivel 2.  
  
> [!NOTE]
>  Estos niveles tienen requisitos diferentes que los niveles de compatibilidad de la API de ODBC del mismo nombre en el 2 de ODBC *.x*. En concreto, todas las características implícito en el 2 de ODBC *.x* conformidad 1 nivel de API ahora forman parte del nivel de conformidad de interfaz de núcleo. Como resultado, muchos controladores ODBC pueden notificar el cumplimiento de la interfaz de nivel básico.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Conformidad de interfaz de núcleo](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Cumplimiento de la interfaz de nivel 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformidad de función](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformidad de atributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformidad de campo de descriptor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
