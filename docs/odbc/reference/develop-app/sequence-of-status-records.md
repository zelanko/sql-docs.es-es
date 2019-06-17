---
title: Secuencia de registros de estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17a88095611a5f551708f3950359063317368757
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62465924"
---
# <a name="sequence-of-status-records"></a>Secuencia de registros de estado
Si se devuelven dos o más registros de estado, el Administrador de controladores y el controlador clasificarán según las reglas siguientes. El registro con la clasificación más alta es el primer registro. No se considera el origen de un registro (Administrador de controladores, controladores, puerta de enlace etc.) cuando los registros de categoría.  
  
-   **Errores** registros de estado que se describen los errores tienen la clasificación más alta. Entre los registros de error, los registros que indican un error de transacción o un error en la transacción posibles outrank todos los demás registros. Si dos o más registros de describen la misma condición de error, SQLSTATE definido por la especificación de CLI de grupo abierto (clases 03 a través de HZ) outrank SQLSTATEs definidos por el controlador y definidas por ODBC.  
  
-   **Los valores de datos No definido por la implementación** registros de estado que describen los valores de datos No definidos por el controlador (clase 02) tienen la segunda clasificación más alta.  
  
-   **Advertencias** registros de estado que describen advertencias (clase 01) tienen el rango más bajo. Si dos o más registros describen la misma condición de advertencia advertencia SQLSTATE definido por la especificación de CLI de grupo abierto outrank SQLSTATEs definidos por el controlador y definidas por ODBC.  
  
 Si hay dos o más registros con la clasificación más alta, no se define qué registro es el primero. El orden de todos los demás registros es indefinido. En concreto, ya que pueden aparecer advertencias antes de errores, las aplicaciones deben comprobar todos los registros de estado cuando una función devuelve un valor distinto de SQL_SUCCESS.
