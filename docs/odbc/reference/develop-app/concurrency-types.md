---
title: Tipos de simultaneidad | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 737fadc881109457051cf30bfce9b493bd164f1c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="concurrency-types"></a>Tipos de simultaneidad
Para solucionar el problema de una simultaneidad reducida en los cursores, ODBC expone cuatro tipos diferentes de simultaneidad de cursor:  
  
-   **Sólo lectura** el cursor puede leer los datos, pero no se puede actualizar o eliminar datos. Este es el tipo de simultaneidad predeterminado. Aunque el DBMS pueden bloquear filas para exigir los niveles de aislamiento Serializable y lectura repetible, pueden usar bloqueos de lectura en lugar de bloqueos de escritura. Esto supone una mayor simultaneidad porque otras transacciones al menos pueden leer los datos.  
  
-   **Bloqueo** el cursor utiliza el nivel más bajo de bloqueo es necesario para asegurarse de que puede actualizar o eliminar filas del conjunto de resultados. Esto produce normalmente en los niveles de simultaneidad muy bajo, especialmente en los niveles de aislamiento de transacción Repeatable Read y Serializable.  
  
-   **Simultaneidad optimista con versiones de fila y simultaneidad optimista con valores** el cursor utiliza simultaneidad optimista: actualiza o elimina las filas únicamente si no han cambiado desde su última lectura. Para detectar los cambios, compara las versiones de fila o valores. No hay ninguna garantía de que el cursor podrá actualizar o eliminar una fila, pero es mucho mayor que cuando se utiliza el bloqueo de simultaneidad. Para obtener más información, vea la sección siguiente, [simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Una aplicación especifica qué tipo de simultaneidad desea que el cursor va a utilizar con el atributo de instrucción SQL_ATTR_CONCURRENCY. Para determinar qué tipos se admiten, llama a **SQLGetInfo** con la opción SQL_SCROLL_CONCURRENCY.

