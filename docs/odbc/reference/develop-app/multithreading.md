---
title: Multithreading (Multithreading) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10d1b401ac780d24184c4c2337199e99973e916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302423"
---
# <a name="multithreading"></a>Subprocesamiento múltiple
En los sistemas operativos multiproceso, los controladores deben ser seguros para subprocesos. Es decir, debe ser posible que las aplicaciones usen el mismo identificador en más de un subproceso. La forma en que se logra esto es específica del controlador y es probable que los controladores serializarán cualquier intento de usar simultáneamente el mismo identificador en dos subprocesos diferentes.  
  
 Las aplicaciones suelen usar varios subprocesos en lugar de procesamiento asincrónico. La aplicación crea un subproceso independiente, llama a una función ODBC en él y, a continuación, continúa el procesamiento en el subproceso principal. En lugar de tener que sondear continuamente la función asincrónica, como es el caso cuando se usa el atributo de instrucción SQL_ATTR_ASYNC_ENABLE, la aplicación simplemente puede dejar que finalice el subproceso recién creado.  
  
 Las funciones que aceptan un identificador de instrucción y se ejecutan en un subproceso se pueden cancelar llamando a **SQLCancel** con el mismo identificador de instrucción desde otro subproceso. Aunque los controladores no deben serializar el uso de **SQLCancel** de esta manera, no hay ninguna garantía de que llamar a **SQLCancel** cancelará realmente la función que se ejecuta en el otro subproceso.
