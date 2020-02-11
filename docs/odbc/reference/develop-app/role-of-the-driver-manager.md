---
title: Rol del administrador de controladores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7184c8ac9e0ad1813999a276f1579351f98544ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020400"
---
# <a name="role-of-the-driver-manager"></a>Rol del Administrador de controladores
El administrador de controladores determina el orden final en el que se devuelven los registros de estado que genera. En concreto, determina qué registro tiene el rango más alto y se devuelve en primer lugar. El controlador es responsable de la ordenación de los registros de estado que genera. Si el administrador de controladores y el controlador publican registros de estado, el administrador de controladores es responsable de ordenarlos. Para obtener más información, consulte [sequence of status Records](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 El administrador de controladores realiza tantas comprobaciones de errores como pueda. Esto evita que todos los controladores comprueben los mismos errores. Por ejemplo, si un argumento de función acepta un número discreto de valores, como *operación* en **SQLSetPos**, el administrador de controladores comprueba que el valor especificado es válido.  
  
 En las secciones siguientes se describen los tipos de condiciones que comprueba el administrador de controladores. No pretende ser exhaustiva; para obtener una lista completa del SQLSTATEs que devuelve el administrador de controladores, consulte la sección "diagnósticos" de cada función. la descripción de cada comprobación realizada por el administrador de controladores comienza con las letras "(DM)". Vea también las tablas de transición de estado en el [Apéndice B: tablas de transición de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); el administrador de controladores detecta los errores que se muestran entre paréntesis.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Comprobaciones de valores de argumento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Comprobaciones de transición de estado](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Comprobaciones de errores generales](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Error del Administrador de controladores y las comprobaciones de advertencia](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
