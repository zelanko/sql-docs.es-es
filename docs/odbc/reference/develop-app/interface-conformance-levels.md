---
title: Niveles de cumplimiento de la interfaz | Microsoft Docs
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
ms.openlocfilehash: 185e68ed8d083e3ccfbab99369f6a778766a4c09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138910"
---
# <a name="interface-conformance-levels"></a>Niveles de compatibilidad de interfaz
El propósito de la redistribución es informar a la aplicación de qué características están disponibles en el controlador. Un esquema de nivelación basado en funciones no logra de manera suficiente este objetivo. En ODBC 3. *x*, los controladores se clasifican en función de las características que poseen. La compatibilidad con la característica puede incluir compatibilidad con la función. también puede incluir compatibilidad con un campo de descriptor, un atributo de instrucción, un valor "Y" para un tipo de información devuelto por **SQLGetInfo**, etc.  
  
 Para simplificar la especificación del cumplimiento de la interfaz, ODBC define tres niveles de cumplimiento. Para cumplir un determinado nivel de cumplimiento, un controlador debe cumplir todos los requisitos de ese nivel de cumplimiento. La conformidad con un nivel determinado implica una conformidad completa con todos los niveles inferiores.  
  
 Los niveles de cumplimiento no siempre se dividen en compatibilidad con una lista específica de funciones ODBC, sino que especifican las características admitidas como se indica en las secciones siguientes. Para proporcionar compatibilidad con una característica, un controlador debe admitir algunas o todas las formas de llamadas a determinadas funciones de ODBC (para obtener más información, vea [conformidad con funciones](../../../odbc/reference/develop-app/function-conformance.md)), establecer ciertos atributos (vea [cumplimiento de atributos](../../../odbc/reference/develop-app/attribute-conformance.md)) y ciertos campos de descriptor (vea conformidad del [Campo descriptor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 La aplicación detecta el nivel de conformidad de la interfaz de un controlador mediante la conexión a un origen de datos y la llamada a **SQLGetInfo** con la opción SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Los controladores son gratuitos para implementar características más allá del nivel al que notifican la conformidad completa. Las aplicaciones detectan estas capacidades adicionales mediante una llamada a **SQLGetFunctions** (para determinar qué funciones ODBC están presentes) y a **SQLGetInfo** (para consultar otras funciones de ODBC).  
  
 Hay tres niveles de cumplimiento de la interfaz ODBC: Core, nivel 1 y nivel 2.  
  
> [!NOTE]
>  Estos niveles de conformidad tienen requisitos diferentes a los niveles de compatibilidad de la API de ODBC del mismo nombre en ODBC 2 *. x*. En concreto, todas las características implícitas por el nivel de conformidad de la API de ODBC 2 *. x* son parte del nivel de cumplimiento de la interfaz principal. Como resultado, muchos controladores ODBC pueden informar del cumplimiento de la interfaz de nivel básico.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Conformidad de interfaz de núcleo](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Cumplimiento de la interfaz de nivel 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformidad de función](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformidad de atributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformidad de campo de descriptor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
