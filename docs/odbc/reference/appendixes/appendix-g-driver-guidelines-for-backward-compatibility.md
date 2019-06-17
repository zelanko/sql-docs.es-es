---
title: 'Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d78de7b3bd1d91351a4159847d6605e30cc1353d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026632"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores
En este apéndice se proporciona información para los escritores de controladores que trabaja en ODBC 3. *x* controladores que necesitan compatibilidad con ODBC 2. *x* aplicaciones. Para obtener más información sobre la compatibilidad con versiones anteriores, consulte [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores de controladores ODBC 3.x](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) -nuevas características son características que existen en ODBC 3. *x* y no en ODBC 2. *x*. ODBC 3. *x* controladores generalmente no es necesario preocuparse por mantener la compatibilidad con las nuevas características porque ODBC 2. *x* nunca utilizarlos las aplicaciones. El único excepciones a esto son las características relacionadas con **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, y **SQLExtendedFetch**; para obtener más información Para más información, vea más adelante en este apéndice.  
  
-   [Asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) -características duplicados son características que se implementan de forma diferente en ODBC 3. *x* y ODBC 2. *x*. ODBC 3. *x* controladores no tiene que preocuparse por mantener la compatibilidad con características duplicados porque siempre se asigna el Administrador de controladores ODBC 2. *x* características que ODBC 3. *x* características cuando se llama a una aplicación ODBC 3. *x* controlador. Por lo tanto, un ODBC 3. *x* controlador ve solo ODBC 3. *x* características. Para obtener más información acerca de estas asignaciones, más adelante en este apéndice, vea.  
  
-   [Cambios de comportamiento y controladores ODBC 3.x](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) -cambios de comportamiento son características que se tratan de forma diferente en ODBC 3. *x* y ODBC 2. *x*. ODBC 3. *x* controladores tienen que preocuparse por los cambios de comportamiento y actuar en respuesta al atributo SQL_ATTR_ODBC_VERSION entorno establecido por la aplicación.
