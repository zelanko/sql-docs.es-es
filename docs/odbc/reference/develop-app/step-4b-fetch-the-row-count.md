---
description: 'Paso 4b: Captura del recuento de filas'
title: 'PASO 4B: capturar el recuento de filas | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eab5e1e1bf7eba70e2d84b36349e2f982a0b14c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494608"
---
# <a name="step-4b-fetch-the-row-count"></a>Paso 4b: Captura del recuento de filas
El siguiente paso consiste en capturar el recuento de filas, tal y como se muestra en la siguiente ilustración.  
  
 ![Muestra la captura del recuento de filas](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 Si la instrucción ejecutada en el paso 3 era una instrucción **Update**, **Delete**o **Insert** , la aplicación recupera el recuento de las filas afectadas con **SQLRowCount**. Para obtener más información, vea [determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 La aplicación ahora vuelve al paso 3 para ejecutar otra instrucción en la misma transacción o continúa en el paso 5 para confirmar o revertir la transacción.
