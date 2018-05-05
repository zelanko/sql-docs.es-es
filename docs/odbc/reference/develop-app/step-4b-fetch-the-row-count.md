---
title: 'Paso 4b: capturar el recuento de filas | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b90259758ceab600abce600bdfdab6edc52f506
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="step-4b-fetch-the-row-count"></a>Paso 4b: capturar el recuento de filas
El paso siguiente es capturar el recuento de filas, como se muestra en la siguiente ilustración.  
  
 ![Muestra cómo recuperar el recuento de filas](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 Si la instrucción ejecutada en el paso 3 fue un **actualización**, **eliminar**, o **insertar** (instrucción), la aplicación recupera el recuento de filas afectadas con  **SQLRowCount**. Para obtener más información, consulte [determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 Ahora, la aplicación vuelve al paso 3 para ejecutar otra instrucción en la misma transacción o continúa con el paso 5 para confirmar o revertir la transacción.
