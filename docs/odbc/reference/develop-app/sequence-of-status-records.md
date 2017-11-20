---
title: Secuencia de registros de estado | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0e11fdd0d5d560cfcacd034745f7ed32cf8fca8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sequence-of-status-records"></a>Secuencia de registros de estado
Si se devuelven dos o más registros de estado, el Administrador de controladores y el controlador clasifican según las reglas siguientes. El registro con la clasificación más alta es el primer registro. El origen de un registro (Administrador de controladores, controladores, puerta de enlace etc.) no se considera cuando los registros de categoría.  
  
-   **Errores** registros de estado que se describen los errores tienen la clasificación más alta. Entre los registros de error, los registros que indican un error de transacción o transacciones posible error outrank todos los demás registros. Si dos o más registros de describen la misma condición de error, SQLSTATE definido por la especificación de CLI de grupo abierto (clases 03 a través de HZ) outrank SQLSTATE definida por ODBC y definidos por el controlador.  
  
-   **Los valores de datos No definido por la implementación** registros de estado que se describen los valores de datos No definidos por el controlador (clase 02) tienen la segunda clasificación más alta.  
  
-   **Advertencias** registros de estado que describen las advertencias (clase 01) tienen el rango más bajo. Si dos o más registros describen la misma condición de advertencia advertencia SQLSTATE definido por la especificación de CLI de grupo abierto outrank SQLSTATE definida por ODBC y definidos por el controlador.  
  
 Si hay dos o más registros con la clasificación más alta, no se define cuál de los registros es el primer registro. El orden de todos los demás registros es indefinido. En particular, porque pueden aparecer advertencias antes de errores, las aplicaciones deben comprobar todos los registros de estado cuando una función devuelve un valor distinto de SQL_SUCCESS.

