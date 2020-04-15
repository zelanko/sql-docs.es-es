---
title: Función del Administrador de controladores ( Driver Manager) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee3d704ea43125c3cd912a4e67d90bf5d50c733e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304306"
---
# <a name="role-of-the-driver-manager"></a>Rol del Administrador de controladores
El Administrador de controladores determina el orden final en el que se devuelven los registros de estado que genera. En particular, determina qué registro tiene el rango más alto y se debe devolver primero. El controlador es responsable de ordenar los registros de estado que genera. Si el Administrador de controladores y el controlador registran los registros de estado, el Administrador de controladores es responsable de ordenarlos. Para obtener más información, consulte [Secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 El Administrador de controladores hace tanto error de comprobación como puede. Esto evita que todos los controladores comprueben los mismos errores. Por ejemplo, si un argumento de función acepta un número discreto de valores, como *Operation* en **SQLSetPos**, el Administrador de controladores comprueba que el valor especificado es legal.  
  
 En las secciones siguientes se describen los tipos de condiciones comprobadas por el Administrador de controladores. No pretenden ser exhaustivas; para obtener una lista completa de los SQLSTATEs que devuelve el Administrador de controladores, consulte la sección "Diagnóstico" de cada función; la descripción de cada cheque realizado por el Administrador de conductores comienza con las letras "(DM)." Consulte también las tablas de transición de estado en [el Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC; los errores mostrados entre paréntesis son detectados por el Administrador de controladores.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Comprobaciones de valores de argumento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Comprobaciones de transición de estado](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Comprobaciones de errores generales](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Error del Administrador de controladores y las comprobaciones de advertencia](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
