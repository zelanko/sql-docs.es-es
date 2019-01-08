---
title: Precisión del tipo de datos de intervalo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8df4339ae30b9058e5a5864c37807c6b02e4fdd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532119"
---
# <a name="interval-data-type-precision"></a>Precisión del tipo de datos de intervalo
Precisión para un tipo de datos de intervalo incluye iniciales de precisión, la precisión de intervalo y la precisión de segundos del intervalo.  
  
 El campo inicial de un intervalo es un valor numérico con signo. El número máximo de dígitos para el campo inicial viene determinada por una cantidad llamada *precisión, del principio del intervalo* que forma parte de la declaración de tipos de datos. Por ejemplo, la declaración: INTERVALO HOUR(5) al minuto tiene una precisión de intervalo inicial de 5; el campo de hora puede tomar los valores de-99999 y 99999. El intervalo de precisión del principio se incluye en el campo SQL_DESC_DATETIME_INTERVAL_PRECISION del registro de descriptor.  
  
 Se llama a la lista de campos de un tipo de datos de intervalo se compone de *precisión de intervalo*. No es un valor numérico, como el término "precisión" pueda implicar. Por ejemplo, la precisión de intervalo del tipo INTERVAL DAY TO en segundo lugar es la lista de día, hora, minuto, segundo. No hay ningún campo de descriptor que contiene este valor; la precisión de intervalo siempre se puede determinar mediante el tipo de datos de intervalo.  
  
 Cualquier tipo de datos de intervalo que tiene un segundo campo tiene un *precisión de segundos*. Este es el número de dígitos decimales que se permiten en la parte fraccionaria del valor de segundos. Esto es diferente para otros tipos de datos, donde la precisión indica el número de dígitos anteriores al separador decimal. La precisión de segundos de un tipo de datos de intervalo es el número de dígitos después del separador decimal. Por ejemplo, si se establece la precisión de segundos a 6, el número 123456 en el campo de fracción se interpretaría como.123456 y el número 1230 se interpretaría como.001230. Para otros tipos de datos, esto se conoce como escalado. Precisión de segundos de intervalo se encuentra en el campo SQL_DESC_PRECISION del descriptor. Si la precisión del componente de fracciones de segundos del valor de intervalo SQL es mayor que lo que puede incluirse en la estructura de intervalo de C, se está definido por controlador si el valor de fracciones de segundo en el intervalo de SQL se redondean o truncan cuando se convierten a C estructura de intervalo.  
  
 Cuando se establece el campo SQL_DESC_CONCISE_TYPE en un tipo de datos de intervalo, se establece el campo SQL_DESC_TYPE en SQL_INTERVAL y el SQL_DESC_DATETIME_INTERVAL_CODE se establece en el código para el tipo de datos de intervalo. El campo SQL_DESC_DATETIME_INTERVAL_PRECISION se establece automáticamente en la precisión inicial de intervalo predeterminado de 2 y el campo SQL_DESC_PRECISION se establece automáticamente en la precisión de segundos de intervalo predeterminado de 6. Si alguno de estos valores no es adecuado, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField**.
