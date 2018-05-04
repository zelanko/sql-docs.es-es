---
title: Notas de seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a99ddfed60ebb9d7d8dcfd4215b7c0a8d57314fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Notas de seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle es segura para subprocesos; Sin embargo, Oracle no admite varias instrucciones simultáneas en una sola conexión. El controlador aplica esta restricción. En otras palabras, en las aplicaciones multiproceso, aunque cualquier subproceso puede llamar en el controlador ODBC para Oracle en cualquier momento, el controlador bloquea ningún otro subproceso del controlador en la misma conexión hasta que el subproceso original deja el controlador.  
  
 El controlador no se bloquea si hay dos instrucciones en dos conexiones diferentes. Sin embargo, si hay una sola conexión con dos instrucciones, es posible para el bloqueo.
