---
title: "Los cursores desplazables y aislamiento de transacción | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
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
ms.openlocfilehash: 6c9e38f4287a8832d8e794940093ce696ac0eaf7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
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
|Insert|Quizá [b]|no|no|no|no|no|  
|Update|Quizá [b]|no|no|no|no|no|  
|DELETE|Quizá [b]|no|no|no|no|no|  
|Dirigido por conjuntos de claves|||||||  
|Insert|Quizá [b]|no|no|no|no|no|  
|Update|Sí|Sí|Sí|Sí|no|no|  
|DELETE|Quizá [b]|Sí|Sí|Sí|no|no|  
|Dinámica|||||||  
|Insert|Sí|Sí|Sí|Sí|Sí|no|  
|Update|Sí|Sí|Sí|Sí|no|no|  
|DELETE|Sí|Sí|Sí|Sí|no|no|  
  
 [a] las letras entre paréntesis indican el nivel de aislamiento de la transacción que contiene el cursor; el nivel de aislamiento de la otra transacción (en el que se realizó el cambio) es irrelevante.  
  
 RU: Lectura no confirmada  
  
 RC: Lectura confirmada  
  
 RR: Lectura repetible  
  
 S: Serializable  
  
 [b] depende de cómo se implementa el cursor. Si el cursor puede detectar dichos cambios se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.
