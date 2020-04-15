---
title: Precisión del tipo de datos de intervalo ( Interval Data Type Precision ) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 746293c545c47917abd084ec3eb105051fc2fbcf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290745"
---
# <a name="interval-data-type-precision"></a>Precisión del tipo de datos de intervalo
La precisión de un tipo de datos de intervalo incluye precisión inicial de intervalo, precisión de intervalo y precisión de segundos.  
  
 El campo inicial de un intervalo es un número con signo. El número máximo de dígitos para el campo inicial viene determinado por una cantidad denominada precisión inicial de *intervalo,* que forma parte de la declaración de tipo de datos. Por ejemplo, la declaración: INTERVAL HOUR(5) TO MINUTE tiene una precisión inicial de intervalo de 5; el campo HOUR puede tomar valores de -99999 a 99999. La precisión inicial del intervalo se encuentra en el campo SQL_DESC_DATETIME_INTERVAL_PRECISION del registro descriptor.  
  
 La lista de campos de los que se compone un tipo de datos de intervalo se denomina precisión de *intervalo.* No es un valor numérico, como el término "precisión" podría implicar. Por ejemplo, la precisión del intervalo del tipo INTERVAL DAY TO SECOND es la lista DAY, HOUR, MINUTE, SECOND. No hay ningún campo descriptor que contenga este valor; la precisión del intervalo siempre se puede determinar por el tipo de datos de intervalo.  
  
 Cualquier tipo de datos de intervalo que tenga un campo SECOND tiene una precisión de *segundos.* Este es el número de dígitos decimales permitidos en la parte fraccionaria del valor de segundos. Esto es diferente que para otros tipos de datos, donde la precisión indica el número de dígitos antes del punto decimal. La precisión de segundos de un tipo de datos de intervalo es el número de dígitos después del punto decimal. Por ejemplo, si la precisión de segundos se establece en 6, el número 123456 en el campo de fracción se interpretaría como .123456 y el número 1230 se interpretaría como .001230. Para otros tipos de datos, esto se conoce como escala. La precisión de los segundos de intervalo se encuentra en el campo SQL_DESC_PRECISION del descriptor. Si la precisión del componente de fracciones de segundo del valor de intervalo SQL es mayor que la que se puede mantener en la estructura del intervalo C, se define por el controlador si el valor de fracciones de segundo en el intervalo SQL se redondea o trunca cuando se convierte en la estructura del intervalo C.  
  
 Cuando el campo SQL_DESC_CONCISE_TYPE se establece en un tipo de datos de intervalo, el campo SQL_DESC_TYPE se establece en SQL_INTERVAL y el SQL_DESC_DATETIME_INTERVAL_CODE se establece en el código para el tipo de datos de intervalo. El campo SQL_DESC_DATETIME_INTERVAL_PRECISION se establece automáticamente en la precisión inicial del intervalo predeterminado de 2, y el campo SQL_DESC_PRECISION se establece automáticamente en la precisión de los segundos de intervalo predeterminada de 6. Si alguno de estos valores no es adecuado, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField**.
