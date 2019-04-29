---
title: Cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3896473a1fa08f769f13d94bd1d81f373cf67c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026597"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores
La existencia de ambas **SQLFetchScroll** y **SQLExtendedFetch** representa divide entre la aplicación de interfaz de programación (API), que es el conjunto de funciones ODBC sin cifrar primero el las llamadas de aplicación y la interfaz de proveedor de servicio (SPI), que es el conjunto de funciones implementa el controlador. Esta división es necesaria para que ODBC 3. *x*, que usa **SQLFetchScroll**, bealigned con los estándares y también sea compatible con ODBC 2. *x*, que usa **SQLExtendedFetch**.  
  
 El 3 de ODBC *.x* API, que es el conjunto de funciones de la aplicación llama, incluye **SQLFetchScroll** y relacionados con los atributos de instrucción. El 3 de ODBC *.x* SPI, que es el conjunto de funciones implementa el controlador, incluye **SQLFetchScroll**, **SQLExtendedFetch**y relacionados con los atributos de instrucción. Dado que ODBC no aplica esta diferencia entre la API y el SPI formalmente, es posible que ODBC 3 *.x* las aplicaciones llamen a **SQLExtendedFetch** y relacionados con los atributos de instrucción. Sin embargo, no hay ninguna razón para ODBC 3 *.x* aplicación para hacer esto. Para obtener más información acerca de las API y SPI, vea la introducción a [arquitectura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obtener información sobre qué funciones y la instrucción de atributos de una aplicación ODBC 3. *x* aplicación debe usar con los cursores desplazables y de bloque, vea [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Lo que hace el Administrador de controladores](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [Lo que hace el controlador](../../../odbc/reference/appendixes/what-the-driver-does.md)
