---
title: Subprocesamiento múltiple | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a16262d562ca2088f38cd863a6f44e537e65d40
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622173"
---
# <a name="multithreading"></a>Subprocesamiento múltiple
En sistemas operativos multiproceso, los controladores deben ser seguros para subprocesos. Es decir, debe ser posible las aplicaciones utilicen el mismo identificador en más de un subproceso. Forma de conseguirlo es específica del controlador, y es probable que los controladores serializarán cualquier intento de utilizar simultáneamente el mismo identificador en dos subprocesos diferentes.  
  
 Las aplicaciones suelen usar varios subprocesos en lugar de procesamiento asincrónico. La aplicación crea un subproceso independiente, llama a una función ODBC en él y, a continuación, continúa el procesamiento en el subproceso principal. En lugar de tener que sondear continuamente la función asincrónica, como es el caso cuando se usa el atributo de instrucción SQL_ATTR_ASYNC_ENABLE, la aplicación puede simplemente dejar que el subproceso recién creado Finalizar.  
  
 Las funciones que aceptan un identificador de instrucción se ejecutan en un subproceso pueden cancelarse mediante una llamada a **SQLCancel** con la misma instrucción controlar desde otro subproceso. Aunque los controladores no deben serializar el uso de **SQLCancel** de esta manera, no hay ninguna garantía de que la llamada a **SQLCancel** cancelará realmente la función que se ejecuta en el otro subproceso.
