---
title: Secuencia de registros de estado ( Secuencia de registros de estado) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb26731a85d1d6313658fe9c24a32167b351d2d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304176"
---
# <a name="sequence-of-status-records"></a>Secuencia de registros de estado
Si se devuelven dos o más registros de estado, el Administrador de controladores y el controlador los clasifican de acuerdo con las siguientes reglas. El registro con el rango más alto es el primer registro. El origen de un registro (Administrador de controladores, controlador, puerta de enlace, etc.) no se tiene en cuenta al clasificar registros.  
  
-   **Errores** Los registros de estado que describen los errores tienen el rango más alto. Entre los registros de error, los registros que indican un error de transacción o un posible error de transacción se sube a todos los demás registros. Si dos o más registros describen la misma condición de error, los SQLSTATEs definidos por la especificación de la CLI de grupo abierto (clases 03 a HZ) superarán los SQLSTATEs definidos por ODBC y definidos por el controlador.  
  
-   **Valores sin datos definidos por la implementación** Los registros de estado que describen los valores sin datos definidos por el controlador (clase 02) tienen el segundo rango más alto.  
  
-   **Advertencias** Los registros de estado que describen las advertencias (clase 01) tienen el rango más bajo. Si dos o más registros describen la misma condición de advertencia, los SQLSTATEs de advertencia definidos por la especificación de la CLI de grupo abierto sube a SQLSTATEs definidos por ODBC y definidos por el controlador.  
  
 Si hay dos o más registros con el rango más alto, es indefinido qué registro es el primer registro. El orden de todos los demás registros es indefinido. En particular, dado que pueden aparecer advertencias antes de los errores, las aplicaciones deben comprobar todos los registros de estado cuando una función devuelve un valor distinto de SQL_SUCCESS.
