---
description: Tipos de simultaneidad
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d55740b71d4e9a7d3b8d22400da0c5b3d94e73d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461547"
---
# <a name="concurrency-types"></a>Tipos de simultaneidad
Para solucionar el problema de la simultaneidad reducida en cursores de, ODBC expone cuatro tipos diferentes de simultaneidad de cursores:  
  
-   **Solo lectura** El cursor puede leer datos, pero no puede actualizar o eliminar datos. Este es el tipo de simultaneidad predeterminado. Aunque el DBMS podría bloquear filas para aplicar los niveles de aislamiento REPEATABLE Read y serializable, puede usar bloqueos de lectura en lugar de bloqueos de escritura. Esto da como resultado una mayor simultaneidad porque otras transacciones pueden leer los datos al menos.  
  
-   **Bloqueo** de El cursor utiliza el nivel de bloqueo más bajo necesario para asegurarse de que puede actualizar o eliminar filas en el conjunto de resultados. Esto suele dar como resultado niveles de simultaneidad muy bajos, especialmente en los niveles de aislamiento de transacción REPEATABLE Read y serializable.  
  
-   **Simultaneidad optimista con versiones de fila y simultaneidad optimista usando valores** El cursor usa simultaneidad optimista: actualiza o elimina filas solo si no han cambiado desde que se leyeron por última vez. Para detectar los cambios, compara las versiones de fila o los valores. No hay ninguna garantía de que el cursor pueda actualizar o eliminar una fila, pero la simultaneidad es mucho mayor que cuando se usa el bloqueo. Para obtener más información, vea la siguiente sección, [simultaneidad optimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Una aplicación especifica qué tipo de simultaneidad desea que use el cursor con el atributo de instrucción SQL_ATTR_CONCURRENCY. Para determinar qué tipos se admiten, llama a **SQLGetInfo** con la opción SQL_SCROLL_CONCURRENCY.
