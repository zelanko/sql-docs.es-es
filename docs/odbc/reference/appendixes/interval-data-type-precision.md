---
title: "Precisión del tipo de datos de intervalo | Documentos de Microsoft"
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
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba46b5cc82fd2ac36e9a3cf920b81bc48b0d9baa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="interval-data-type-precision"></a>Precisión del tipo de datos de intervalo
Precisión para un tipo de datos de intervalo incluye intervalo a la precisión, la precisión de intervalo y la precisión de segundos.  
  
 El campo inicial de un intervalo es un tipo numérico con signo. El número máximo de dígitos para el campo inicial se determina por una cantidad llama *precisión, del principio del intervalo* que forma parte de la declaración de tipos de datos. Por ejemplo, la declaración: intervalo HOUR(5) al minuto tiene un intervalo a la precisión de 5; el campo de hora puede tomar los valores de –99999 y 99999. El intervalo de precisión del principio se incluye en el campo SQL_DESC_DATETIME_INTERVAL_PRECISION del registro del descriptor.  
  
 Se llama a la lista de campos de un tipo de datos de intervalo se compone de *precisión de intervalo*. No es un valor numérico, tal y como se podría implica el término "precisión". Por ejemplo, la precisión de intervalo del tipo INTERVAL DAY TO en segundo lugar es la lista día, hora, minuto, segundo. No hay ningún campo de descriptor que contiene este valor; la precisión de intervalo siempre vendrá determinada por el tipo de datos de intervalo.  
  
 Cualquier tipo de datos de intervalo que tiene un segundo campo tiene un *precisión de segundos*. Este es el número de dígitos decimales que se permiten en la parte fraccionaria del valor de los segundos. Esto es diferente de otros tipos de datos, donde la precisión indica el número de dígitos que hay delante del separador decimal. La precisión de segundos de un tipo de datos de intervalo es el número de dígitos después del separador decimal. Por ejemplo, si se establece la precisión de segundos en 6, el número 123456 en el campo de fracción se interpretaría como.123456 y el número 1230 se interpretaría como.001230. Para otros tipos de datos, esto se conoce como escala. Precisión de segundos de intervalo se encuentra en el campo SQL_DESC_PRECISION del descriptor. Si la precisión del componente de fracciones de segundo del valor de intervalo SQL es mayor que lo que se pueden guardar en la estructura de intervalo de C, se está definido por controlador si el valor de fracciones de segundo en el intervalo SQL se redondean o truncan cuando se convierten a C estructura de intervalo.  
  
 Cuando el campo SQL_DESC_CONCISE_TYPE se establece en un tipo de datos de intervalo, el campo SQL_DESC_TYPE se establece en SQL_INTERVAL y el SQL_DESC_DATETIME_INTERVAL_CODE se establece en el código para el tipo de datos de intervalo. El campo SQL_DESC_DATETIME_INTERVAL_PRECISION se establece automáticamente en la precisión iniciales de intervalo predeterminado de 2 y el campo SQL_DESC_PRECISION se establece automáticamente en la precisión de segundos de intervalo predeterminado de 6. Si alguno de estos valores no es adecuado, la aplicación debe establecer explícitamente el campo descriptor a través de una llamada a **SQLSetDescField**.
