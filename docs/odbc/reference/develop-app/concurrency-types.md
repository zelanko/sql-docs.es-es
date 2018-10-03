---
title: Tipos de simultaneidad | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12891d7ee674167157bcb02300d2e4181ef51734
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656460"
---
# <a name="concurrency-types"></a>Tipos de simultaneidad
Para solucionar el problema de simultaneidad reducida en los cursores, ODBC expone cuatro tipos diferentes de simultaneidad de cursor:  
  
-   **Solo lectura** el cursor puede leer los datos, pero no se puede actualizar o eliminar datos. Este es el tipo de simultaneidad predeterminado. Aunque el DBMS podría bloquear filas para exigir los niveles de aislamiento Serializable y lectura repetible, pueden usar bloqueos de lectura en lugar de bloqueos de escritura. Esto da como resultado una mayor simultaneidad porque otras transacciones al menos pueden leer los datos.  
  
-   **Bloqueo** el cursor utiliza el nivel más bajo de bloqueo es necesario para asegurarse de que puede actualizar o eliminar filas del conjunto de resultados. Esto suele generar niveles de simultaneidad muy bajo, especialmente en los niveles de aislamiento de transacción Repeatable Read y Serializable.  
  
-   **Simultaneidad optimista con versiones de fila y la simultaneidad optimista con valores** el cursor utiliza simultaneidad optimista: se actualiza o elimina las filas únicamente si no han cambiado desde que se leyeron por última vez. Para detectar los cambios, compara las versiones de filas o valores. No hay ninguna garantía de que el cursor podrá actualizar o eliminar una fila, pero la simultaneidad es mucho mayor que cuando se utiliza el bloqueo. Para obtener más información, vea la sección siguiente, [simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Una aplicación que especifica qué tipo de simultaneidad desea que el cursor va a utilizar con el atributo de instrucción SQL_ATTR_CONCURRENCY. Para determinar qué tipos se admiten, llama a **SQLGetInfo** con la opción SQL_SCROLL_CONCURRENCY.
