---
title: Cursores desplazables y aislamiento de transacción | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304226"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Los cursores desplazables y aislamiento de transacción
En la tabla siguiente se enumeran los factores que rigen la visibilidad de los cambios.  
  
|Cambios realizados por:|La visibilidad depende de:|  
|----------------------|----------------------------|  
|Cursor|Tipo de cursor, implementación de cursor|  
|Otras instrucciones de la misma transacción|Tipo de cursor|  
|Instrucciones en otras transacciones|Tipo de cursor, nivel de aislamiento de transacción|  
  
 Estos factores se muestran en la siguiente ilustración.  
  
 ![Factores que rigen la visibilidad de los cambios](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 En la tabla siguiente se resume la capacidad de cada tipo de cursor para detectar los cambios realizados por sí mismos, por otras operaciones en su propia transacción y por otras transacciones. La visibilidad de los últimos cambios depende del tipo de cursor y del nivel de aislamiento de la transacción que contiene el cursor.  
  
|Cursor type\action|Propio|Solos<br /><br /> TXN|Othr<br /><br /> TXN<br /><br /> (RU [a])|Othr<br /><br /> TXN<br /><br /> (RC [a])|Othr<br /><br /> TXN<br /><br /> (RR [a])|Othr<br /><br /> TXN<br /><br /> (S [a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|estática|||||||  
|Insertar|Quizás [b]|Sin|Sin|Sin|Sin|No|  
|Actualizar|Quizás [b]|Sin|Sin|Sin|Sin|No|  
|Eliminar|Quizás [b]|Sin|Sin|Sin|Sin|No|  
|Dirigido por conjuntos de claves|||||||  
|Insertar|Quizás [b]|Sin|Sin|Sin|Sin|No|  
|Actualizar|Sí|Sí|Sí|Sí|Sin|No|  
|Eliminar|Quizás [b]|Sí|Sí|Sí|Sin|No|  
|Dinámica|||||||  
|Insertar|Sí|Sí|Sí|Sí|Sí|No|  
|Actualizar|Sí|Sí|Sí|Sí|Sin|No|  
|Eliminar|Sí|Sí|Sí|Sí|Sin|No|  
  
 [a] las letras entre paréntesis indican el nivel de aislamiento de la transacción que contiene el cursor; el nivel de aislamiento de la otra transacción (en la que se realizó el cambio) es irrelevante.  
  
 RU: lectura no confirmada  
  
 RC: lectura confirmada  
  
 RR: lectura repetible  
  
 S: serializable  
  
 [b] depende de cómo se implemente el cursor. El hecho de que el cursor pueda detectar estos cambios se indica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.
