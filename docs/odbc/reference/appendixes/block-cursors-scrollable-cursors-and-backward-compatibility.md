---
title: Cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores . Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe24362f1a49577a7fb494f768947080d0ab6e9e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292315"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores
La existencia de **SQLFetchScroll** y **SQLExtendedFetch** representa la primera división clara en ODBC entre la interfaz de programación de aplicaciones (API), que es el conjunto de funciones que llama la aplicación y la interfaz de proveedor de servicios (SPI), que es el conjunto de funciones que implementa el controlador. Esta división es necesaria para que ODBC *3.x*, que utiliza **SQLFetchScroll**, se alinea con los estándares y también es compatible con ODBC *2.x*, que utiliza **SQLExtendedFetch**.  
  
 La API ODBC *3.x,* que es el conjunto de funciones a las que llama la aplicación, incluye **SQLFetchScroll** y atributos de instrucción relacionados. El SPI de ODBC *3.x,* que es el conjunto de funciones que implementa el controlador, incluye **SQLFetchScroll**, **SQLExtendedFetch**y atributos de instrucción relacionados. Dado que ODBC no aplica formalmente esta división entre la API y el SPI, es posible que las aplicaciones ODBC *3.x* llamen a **SQLExtendedFetch** y atributos de instrucción relacionados. Sin embargo, no hay ninguna razón para que la aplicación ODBC *3.x* haga esto. Para obtener más información acerca de las API y los SPI, vea la introducción a la [arquitectura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obtener información sobre qué funciones y atributos de instrucción debe usar una aplicación ODBC *3.x* con cursores de bloque y desplazables, vea Cursores de [bloque, cursores desplazables y compatibilidad con versiones anteriores para aplicaciones ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Lo que hace el Administrador de controladores](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [Lo que hace el controlador](../../../odbc/reference/appendixes/what-the-driver-does.md)
