---
title: 'Apéndice G: Directrices del controlador para la compatibilidad con versiones anteriores ? Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1055f94cb54bba9262f210e5df5f028029aebf5b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292405"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores
Este apéndice proporciona información para los escritores de controladores que trabajan en ODBC 3. *x* controladores que necesitan admitir ODBC 2. *x* aplicaciones. Para obtener más información acerca de la compatibilidad con versiones anteriores, vea [Compatibilidad con versiones anteriores y Cumplimiento](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)de normas .  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores para controladores ODBC 3.x:](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) las nuevas características son características que existen en ODBC 3. *x* y no en ODBC 2. *x*. ODBC 3. *x* controladores generalmente no tienen que preocuparse por la compatibilidad con versiones anteriores con nuevas características porque ODBC 2. *x* las aplicaciones nunca las utilizan. Las únicas excepciones a esto son características relacionadas con **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**y **SQLExtendedFetch**; para obtener más información, véase , más adelante en este apéndice.  
  
-   [Asignación de funciones en desuso:](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) las características duplicadas son características que se implementan de forma diferente en ODBC 3. *x* y ODBC 2. *x*. ODBC 3. *x* controladores no tienen que preocuparse por la compatibilidad con versiones anteriores con características duplicadas porque el Administrador de controladores siempre asigna ODBC 2. *x* características para ODBC 3. *x* características al llamar a un ODBC 3. *x* conductor. Por lo tanto, un ODBC 3. *x* controlador ve sólo ODBC 3. *x* características. Para obtener más información acerca de estas asignaciones, consulte , más adelante en este apéndice.  
  
-   [Cambios de comportamiento y controladores ODBC 3.x:](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) los cambios de comportamiento son características que se controlan de forma diferente en ODBC 3. *x* y ODBC 2. *x*. ODBC 3. *x* los controladores tienen que preocuparse por los cambios de comportamiento y actuar en respuesta al atributo de entorno SQL_ATTR_ODBC_VERSION establecido por la aplicación.
