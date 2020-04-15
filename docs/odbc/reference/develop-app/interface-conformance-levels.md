---
title: Niveles de conformidad de la interfaz ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff555324746fcb92641126ddf11ea91ce5e3f89
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304605"
---
# <a name="interface-conformance-levels"></a>Niveles de compatibilidad de interfaz
El propósito de la nivelación es informar a la aplicación qué características están disponibles para él desde el controlador. Un esquema de nivelación basado en funciones no logra suficientemente este objetivo. En ODBC 3. *x*, los controladores se clasifican en función de las características que poseen. La compatibilidad con la característica puede incluir la compatibilidad con la función; también puede incluir la compatibilidad con un campo descriptor, un atributo de instrucción, un valor "Y" para un tipo de información devuelto por **SQLGetInfo**, etc.  
  
 Para simplificar la especificación de conformidad de la interfaz, ODBC define tres niveles de conformidad. Para cumplir con un nivel de conformidad determinado, un conductor debe cumplir todos los requisitos de ese nivel de conformidad. La conformidad con un nivel dado implica una conformidad completa con todos los niveles inferiores.  
  
 Los niveles de conformidad no siempre se dividen perfectamente en compatibilidad con una lista específica de funciones ODBC, sino que especifican las características admitidas como se muestra en las secciones siguientes. Para proporcionar compatibilidad con una característica, un controlador debe admitir algunas o todas las formas de llamadas a determinadas funciones ODBC (para obtener más información, vea [Conformidad](../../../odbc/reference/develop-app/function-conformance.md)de funciones ), establecer determinados atributos (consulte [Conformidad](../../../odbc/reference/develop-app/attribute-conformance.md)de atributos ) y determinados campos descriptores (consulte [Conformidad](../../../odbc/reference/develop-app/descriptor-field-conformance.md)de campos descriptores ).  
  
 La aplicación detecta el nivel de conformidad de la interfaz de un controlador mediante la conexión a un origen de datos y llamar a **SQLGetInfo** con la opción SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Los controladores son libres de implementar características más allá del nivel al que reclaman la conformidad completa. Las aplicaciones detectan cualquiera de estas capacidades adicionales mediante una llamada a **SQLGetFunctions** (para determinar qué funciones ODBC están presentes) y **SQLGetInfo** (para consultar varias otras capacidades ODBC).  
  
 Hay tres niveles de conformidad de la interfaz ODBC: Núcleo, Nivel 1 y Nivel 2.  
  
> [!NOTE]
>  Estos niveles de conformidad tienen requisitos diferentes que los niveles de conformidad de la API ODBC del mismo nombre en ODBC 2 *.x*. En particular, todas las características implícitas por ODBC 2 *.x* CONFORMIDAD de API Nivel 1 ahora forman parte del nivel de conformidad de la interfaz principal. Como resultado, muchos controladores ODBC pueden notificar conformidad de interfaz de nivel principal.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Conformidad de interfaz de núcleo](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Cumplimiento de la interfaz de nivel 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformidad de función](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformidad de atributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformidad de campo de descriptor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
