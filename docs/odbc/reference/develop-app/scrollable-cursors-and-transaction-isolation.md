---
title: Cursores desplazables y aislamiento de transacciones ( Transaction Isolation) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e40278bd209132736aee2788b5648ffa84a44e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304226"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Los cursores desplazables y aislamiento de transacción
En la tabla siguiente se enumeran los factores que rigen la visibilidad de los cambios.  
  
|Cambios realizados por:|La visibilidad depende de:|  
|----------------------|----------------------------|  
|Cursor|Tipo de cursor, implementación del cursor|  
|Otros estados de cuenta en la misma transacción|Tipo de cursor|  
|Estados de cuenta en otras transacciones|Tipo de cursor, nivel de aislamiento de transacción|  
  
 Estos factores se muestran en la siguiente ilustración.  
  
 ![Factores que rigen la visibilidad de los cambios](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 En la tabla siguiente se resume la capacidad de cada tipo de cursor para detectar los cambios realizados por sí mismo, por otras operaciones en su propia transacción y por otras transacciones. La visibilidad de estos últimos cambios depende del tipo de cursor y del nivel de aislamiento de la transacción que contiene el cursor.  
  
|Tipo de cursor-acción|Propio|Propio<br /><br /> Txn|Othr<br /><br /> Txn<br /><br /> (RU[a])|Othr<br /><br /> Txn<br /><br /> (RC[a])|Othr<br /><br /> Txn<br /><br /> (RR[a])|Othr<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|estática|||||||  
|Insertar|Tal vez[b]|Sin|Sin|Sin|Sin|No|  
|Actualizar|Tal vez[b]|Sin|Sin|Sin|Sin|No|  
|Eliminar|Tal vez[b]|Sin|Sin|Sin|Sin|No|  
|Dirigido por conjuntos de claves|||||||  
|Insertar|Tal vez[b]|Sin|Sin|Sin|Sin|No|  
|Actualizar|Sí|Sí|Sí|Sí|Sin|No|  
|Eliminar|Tal vez[b]|Sí|Sí|Sí|Sin|No|  
|Dinámica|||||||  
|Insertar|Sí|Sí|Sí|Sí|Sí|No|  
|Actualizar|Sí|Sí|Sí|Sí|Sin|No|  
|Eliminar|Sí|Sí|Sí|Sí|Sin|No|  
  
 [a] Las letras entre paréntesis indican el nivel de aislamiento de la transacción que contiene el cursor; el nivel de aislamiento de la otra transacción (en la que se realizó el cambio) es irrelevante.  
  
 RU: Leer sin compromiso  
  
 RC: Leer comprometido  
  
 RR: Lectura repetible  
  
 S: Serializable  
  
 [b] Depende de cómo se implemente el cursor. Si el cursor puede detectar estos cambios se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.
