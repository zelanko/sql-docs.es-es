---
title: Cursores de bloque, los cursores desplazables y compatibilidad con versiones anteriores | Documentos de Microsoft
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
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e25e546b359dd7178739e074664c3239fcfbdba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores
La existencia de ambos **SQLFetchScroll** y **SQLExtendedFetch** representa el primer clear divide en ODBC entre la aplicación de interfaz de programación (API), que es el conjunto de funciones de la las llamadas de la aplicación y la interfaz de proveedor de servicio (SPI), que es el conjunto de funciones el controlador implementa. Esta división es necesaria para que ODBC 3. *x*, que usa **SQLFetchScroll**, bealigned con los estándares y también ser compatibles con ODBC 2. *x*, que usa **SQLExtendedFetch**.  
  
 ODBC 3*.x* API, que es el conjunto de funciones de la aplicación llama, incluye **SQLFetchScroll** y relacionados con los atributos de instrucción. ODBC 3*.x* SPI, que es el conjunto de funciones implementa el controlador, incluye **SQLFetchScroll**, **SQLExtendedFetch**y relacionados con los atributos de instrucción. Dado que ODBC no exige formalmente esta división entre la API y el SPI, es posible que ODBC 3*.x* las aplicaciones llamen a **SQLExtendedFetch** y relacionados con los atributos de instrucción. Sin embargo, no hay ninguna razón para ODBC 3*.x* aplicación para hacer esto. Para obtener más información acerca de las API y el SPI, vea la introducción a [arquitectura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obtener información sobre qué funciones y la declaración de atributos de una aplicación ODBC 3. *x* aplicación debe utilizar con los cursores desplazables y el bloque, vea [cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Lo que hace el Administrador de controladores](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [Lo que hace el controlador](../../../odbc/reference/appendixes/what-the-driver-does.md)
