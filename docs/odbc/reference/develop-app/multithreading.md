---
title: Multithreading | Microsoft Docs
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
ms.openlocfilehash: 1eaa07ce22436bc8bfae215c0431480081ee0f06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086351"
---
# <a name="multithreading"></a>Subprocesamiento múltiple
En los sistemas operativos multiproceso, los controladores deben ser seguros para subprocesos. Es decir, debe ser posible que las aplicaciones usen el mismo identificador en más de un subproceso. El modo en que esto se consigue es específico del controlador y es probable que los controladores serialicen los intentos de usar simultáneamente el mismo identificador en dos subprocesos diferentes.  
  
 Las aplicaciones suelen usar varios subprocesos en lugar del procesamiento asincrónico. La aplicación crea un subproceso independiente, llama a una función ODBC en él y, a continuación, continúa el procesamiento en el subproceso principal. En lugar de tener que sondear continuamente la función asincrónica, como es el caso cuando se usa el atributo de instrucción SQL_ATTR_ASYNC_ENABLE, la aplicación puede simplemente dejar que el subproceso recién creado finalice.  
  
 Las funciones que aceptan un identificador de instrucción y que se ejecutan en un subproceso se pueden cancelar llamando a **SQLCancel** con el mismo identificador de instrucción de otro subproceso. Aunque los controladores no deben serializar el uso de **SQLCancel** de esta manera, no hay ninguna garantía de que la llamada a **SQLCancel** cancele realmente la función que se ejecuta en el otro subproceso.
