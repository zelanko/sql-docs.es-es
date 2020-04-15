---
title: Notas de seguridad de subprocesos sobre las funciones de API (controlador ODBC para Oracle) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 489f0e99ea53d419ff94dddfeb22e37573abb874
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303076"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Notas de seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle es seguro para subprocesos; sin embargo, Oracle no permite varias instrucciones simultáneas en una sola conexión. El controlador aplica esta restricción. En otras palabras, en aplicaciones multiproceso, aunque cualquier subproceso puede llamar al controlador ODBC para Oracle en cualquier momento, el controlador bloquea cualquier otro subproceso del controlador en la misma conexión hasta que el subproceso original sale del controlador.  
  
 El controlador no se bloquea si hay dos instrucciones en dos conexiones diferentes. Sin embargo, si hay una sola conexión con dos instrucciones, hay posibilidad de bloqueo.
