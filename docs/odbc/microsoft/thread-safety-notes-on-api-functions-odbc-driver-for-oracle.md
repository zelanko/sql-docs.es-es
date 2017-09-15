---
title: Notas de seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cc4a28976342768f5c7b2d1cfe8a1d3be6544306
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Notas de seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle es segura para subprocesos; Sin embargo, Oracle no admite varias instrucciones simultáneas en una sola conexión. El controlador aplica esta restricción. En otras palabras, en las aplicaciones multiproceso, aunque cualquier subproceso puede llamar en el controlador ODBC para Oracle en cualquier momento, el controlador bloquea ningún otro subproceso del controlador en la misma conexión hasta que el subproceso original deja el controlador.  
  
 El controlador no se bloquea si hay dos instrucciones en dos conexiones diferentes. Sin embargo, si hay una sola conexión con dos instrucciones, es posible para el bloqueo.
