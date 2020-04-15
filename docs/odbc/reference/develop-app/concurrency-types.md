---
title: Tipos de simultaneidad ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 642301d09c5aa189276db534e58aca0c5e00e3ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299105"
---
# <a name="concurrency-types"></a>Tipos de simultaneidad
Para resolver el problema de la simultaneidad reducida en los cursores, ODBC expone cuatro tipos diferentes de simultaneidad de cursor:  
  
-   **Solo lectura** El cursor puede leer datos, pero no puede actualizar ni eliminar datos. Este es el tipo de simultaneidad predeterminado. Aunque el DBMS puede bloquear filas para aplicar los niveles de aislamiento de lectura repetible y serializable, puede usar bloqueos de lectura en lugar de bloqueos de escritura. Esto da como resultado una mayor simultaneidad porque otras transacciones pueden al menos leer los datos.  
  
-   **Bloqueo** El cursor utiliza el nivel más bajo de bloqueo necesario para asegurarse de que puede actualizar o eliminar filas en el conjunto de resultados. Esto suele tener como resultado niveles de simultaneidad muy bajos, especialmente en los niveles de aislamiento de transacción de lectura repetible y serializable.  
  
-   **Simultaneidad optimista mediante versiones de fila y simultaneidad optimista mediante valores** El cursor utiliza simultaneidad optimista: actualiza o elimina filas solo si no han cambiado desde la última lectura. Para detectar cambios, compara las versiones o los valores de las filas. No hay ninguna garantía de que el cursor podrá actualizar o eliminar una fila, pero la simultaneidad es mucho mayor que cuando se usa el bloqueo. Para obtener más información, vea la sección siguiente, [Simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Una aplicación especifica qué tipo de simultaneidad desea que el cursor use con el atributo de instrucción SQL_ATTR_CONCURRENCY. Para determinar qué tipos se admiten, llama a **SQLGetInfo** con la opción SQL_SCROLL_CONCURRENCY.
