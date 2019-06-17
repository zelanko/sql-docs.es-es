---
title: 'Paso 4b: Capturar el recuento de filas | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3091d379bca6c061437e7767fdf6f99d69dc9861
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149152"
---
# <a name="step-4b-fetch-the-row-count"></a>Paso 4b: Captura del recuento de filas
El paso siguiente es capturar el recuento de filas, como se muestra en la siguiente ilustración.  
  
 ![Muestra cómo recuperar el recuento de filas](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 Si la instrucción ejecutada en el paso 3 fue un **actualización**, **eliminar**, o **insertar** instrucción, la aplicación recupera el recuento de filas afectadas con  **SQLRowCount**. Para obtener más información, consulte [determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 Ahora, la aplicación vuelve al paso 3 para ejecutar otra instrucción en la misma transacción o avanza al paso 5 para confirmar o revertir la transacción.
