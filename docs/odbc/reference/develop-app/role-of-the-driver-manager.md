---
title: Rol del Administrador de controladores | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 485cd951992ed427461e497c53d17a4f6db24a38
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626103"
---
# <a name="role-of-the-driver-manager"></a>Rol del Administrador de controladores
El Administrador de controladores determina el orden en que se va a devolver registros de estado que genera final. En concreto, determina el registro que tiene la clasificación más alta y se devuelve en primer lugar. El controlador es responsable de ordenar los registros de estado que genera. Si se registran registros de estado por el Administrador de controladores y el controlador, el Administrador de controladores es responsable de ordenarlas. Para obtener más información, consulte [secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 El Administrador de controladores no tanta comprobación de errores como sea posible. Esto guarda todos los controladores de la comprobación de los mismos errores. Por ejemplo, si un argumento de función acepta un número de valores discreto como *operación* en **SQLSetPos**, el Administrador de controladores comprueba que el valor especificado es válido.  
  
 Las siguientes secciones describen los tipos de condiciones activadas por el Administrador de controladores. No pretenden ser exhaustivo; Para obtener una lista completa de la SQLSTATE que devuelve el Administrador de controladores, consulte la sección "Diagnostics" de cada función; la descripción de cada comprobación realizada por el Administrador de controladores se inicia con las letras "(DM)". Consulte también las tablas de transición de estado de [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); errores que se muestran entre paréntesis se detectan mediante el Administrador de controladores.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Comprobaciones de valores de argumento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Comprobaciones de transición de estado](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Comprobaciones de errores generales](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Error del Administrador de controladores y las comprobaciones de advertencia](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
