---
title: Los cursores desplazables y aislamiento de transacción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5510eb58315f70195eb40390edec1766c350fb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468602"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Los cursores desplazables y aislamiento de transacción
En la tabla siguiente se enumera los factores que rigen la visibilidad de los cambios.  
  
|Cambios realizados por:|Visibilidad depende de:|  
|----------------------|----------------------------|  
|Cursor|Tipo de cursor, la implementación de cursores|  
|Otras instrucciones en la misma transacción|Tipo de cursor|  
|Instrucciones en otras transacciones|Tipo de cursor, nivel de aislamiento de transacción|  
  
 Estos factores se muestran en la siguiente ilustración.  
  
 ![Factores que rigen la visibilidad de cambios](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 En la tabla siguiente se resume la capacidad de cada tipo de cursor para detectar los cambios realizados por sí mismo, por otras operaciones en su propia transacción y por otras transacciones. La visibilidad de los cambios de esta última depende del tipo de cursor y el nivel de aislamiento de la transacción que contiene el cursor.  
  
|Cursor type\action|Self|El propietario<br /><br /> Txn|Otros<br /><br /> Txn<br /><br /> (RU[a])|Otros<br /><br /> Txn<br /><br /> (RC[a])|Otros<br /><br /> Txn<br /><br /> (RR[a])|Otros<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Estático|||||||  
|Insert|Tal vez [b]|No|Sin|No|No|Sin|  
|Update|Tal vez [b]|Sin|Sin|Sin|No|No|  
|DELETE|Tal vez [b]|No|Sin|Sin|Sin|Sin|  
|Dirigido por conjuntos de claves|||||||  
|Insert|Tal vez [b]|Sin|Sin|Sin|No|No|  
|Update|Sí|Sí|Sí|Sí|Sin|No|  
|DELETE|Tal vez [b]|Sí|Sí|Sí|Sin|No|  
|Dinámico|||||||  
|Insert|Sí|Sí|Sí|Sí|Sí|Sin|  
|Update|Sí|Sí|Sí|Sí|Sin|Sin|  
|DELETE|Sí|Sí|Sí|Sí|Sin|Sin|  
  
 [a] las letras entre paréntesis indican el nivel de aislamiento de la transacción que contiene el cursor; el nivel de aislamiento de la otra transacción (en el que se realizó el cambio) es irrelevante.  
  
 RU: Lectura no confirmada  
  
 RC: Lectura confirmada  
  
 RR: Lectura repetible  
  
 S:  Serializable  
  
 [b] depende de cómo se implementa el cursor. Si el cursor puede detectar estos cambios se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.
