---
title: "Los cursores desplazables y aislamiento de transacción | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e4db2f357942eb7bab34a17e8f9c03e442731055
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Los cursores desplazables y aislamiento de transacción
En la tabla siguiente se enumera los factores que rigen la visibilidad de los cambios.  
  
|Cambios realizados por:|Visibilidad depende de:|  
|----------------------|----------------------------|  
|Cursor|Tipo de cursor, implementación de cursores|  
|Otras instrucciones en la misma transacción|Tipo de cursor|  
|Instrucciones en otras transacciones|Tipo de cursor, nivel de aislamiento de transacción|  
  
 Estos factores se muestran en la siguiente ilustración.  
  
 ![Factores que rigen la visibilidad de cambios](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 En la tabla siguiente se resume la capacidad de cada tipo de cursor para detectar los cambios realizados por sí mismo, por otras operaciones en su propia transacción y por otras transacciones. La visibilidad de los cambios de esta últimas depende el tipo de cursor y el nivel de aislamiento de la transacción que contiene el cursor.  
  
|Cursor type\action|En sí mismo|El propietario<br /><br /> Transacciones de|Otro<br /><br /> Transacciones de<br /><br /> (RU[a])|Otro<br /><br /> Transacciones de<br /><br /> (RC[a])|Otro<br /><br /> Transacciones de<br /><br /> (RR[a])|Otro<br /><br /> Transacciones de<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Estático|||||||  
|Insert|Quizá [b]|No|No|No|No|No|  
|Update|Quizá [b]|No|No|No|No|No|  
|DELETE|Quizá [b]|No|No|No|No|No|  
|Dirigido por conjuntos de claves|||||||  
|Insert|Quizá [b]|No|No|No|No|No|  
|Update|Sí|Sí|Sí|Sí|No|No|  
|DELETE|Quizá [b]|Sí|Sí|Sí|No|No|  
|Dinámica|||||||  
|Insert|Sí|Sí|Sí|Sí|Sí|No|  
|Update|Sí|Sí|Sí|Sí|No|No|  
|DELETE|Sí|Sí|Sí|Sí|No|No|  
  
 [a] las letras entre paréntesis indican el nivel de aislamiento de la transacción que contiene el cursor; el nivel de aislamiento de la otra transacción (en el que se realizó el cambio) es irrelevante.  
  
 RU: Lectura no confirmada  
  
 RC: Lectura confirmada  
  
 RR: Lectura repetible  
  
 S: Serializable  
  
 [b] depende de cómo se implementa el cursor. Si el cursor puede detectar dichos cambios se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.
