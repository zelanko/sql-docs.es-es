---
title: 'Paso 4b: Obtener el recuento de filas ? Microsoft Docs'
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
ms.openlocfilehash: 31ccbd15ae435165ea007fa9f3c0505c1dcc5aa0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302966"
---
# <a name="step-4b-fetch-the-row-count"></a>Paso 4b: Captura del recuento de filas
El siguiente paso es capturar el recuento de filas, como se muestra en la siguiente ilustración.  
  
 ![Muestra la captura del recuento de filas](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 Si la instrucción ejecutada en el paso 3 era una instrucción **UPDATE**, **DELETE**o **INSERT,** la aplicación recupera el recuento de filas afectadas con **SQLRowCount**. Para obtener más información, consulte [Determinación del número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 La aplicación ahora vuelve al paso 3 para ejecutar otra instrucción en la misma transacción o procede al paso 5 para confirmar o revertir la transacción.
