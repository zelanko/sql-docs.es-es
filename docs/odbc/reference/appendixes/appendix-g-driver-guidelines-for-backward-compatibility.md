---
title: "Apéndice G: controlador directrices para la compatibilidad con versiones anteriores | Documentos de Microsoft"
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
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e326abbc0a10899028bf93d27f219fadd8d7dd29
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Apéndice G: controlador directrices para la compatibilidad con versiones anteriores
Este apéndice proporciona información para los escritores de controladores trabajar en ODBC 3. *x* controladores que necesitan compatibilidad con ODBC 2. *x* aplicaciones. Para obtener más información acerca de la compatibilidad con versiones anteriores, consulte [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores de los controladores ODBC 3.x](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) : nuevas características son características que existen en ODBC 3. *x* y no en ODBC 2. *x*. ODBC 3. *x* controladores generalmente no tiene que preocuparse sobre la compatibilidad con versiones anteriores con nuevas características porque ODBC 2. *x* nunca utilizarlos las aplicaciones. El única excepciones a esto son características relacionadas con **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, y **SQLExtendedFetch**; para obtener más información obtener información, vea, más adelante en este apéndice.  
  
-   [Asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) : duplicado características son las que se implementan de forma diferente en ODBC 3. *x* y ODBC 2. *x*. ODBC 3. *x* controladores no tiene que preocuparse de mantener la compatibilidad con características duplicados porque el Administrador de controladores se asigna siempre ODBC 2. *x* características para ODBC 3. *x* características cuando se llama a una aplicación ODBC 3. *x* controlador. Por lo tanto, un ODBC 3. *x* controlador ve solo ODBC 3. *x* características. Para obtener más información acerca de estas asignaciones, vea más adelante en este apéndice.  
  
-   [Cambios de comportamiento y los controladores ODBC 3.x](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) : cambios de comportamiento son características que se tratan de forma diferente en ODBC 3. *x* y ODBC 2. *x*. ODBC 3. *x* controladores tienen que preocuparse sobre los cambios de comportamiento y actuar en respuesta a los atributos de entorno SQL_ATTR_ODBC_VERSION establecidos por la aplicación.

