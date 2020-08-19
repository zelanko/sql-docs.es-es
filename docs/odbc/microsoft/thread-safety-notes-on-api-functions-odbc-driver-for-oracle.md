---
description: Notas de seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle)
title: Notas sobre la seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle) | Microsoft Docs
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
ms.openlocfilehash: 8c7da346832e2682caa02bdbdae91a1133a9cbaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449087"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Notas de seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Microsoft ODBC driver for Oracle es seguro para subprocesos; sin embargo, Oracle no permite varias instrucciones simultáneas en una sola conexión. El controlador aplica esta restricción. En otras palabras, en aplicaciones multiproceso, aunque cualquier subproceso puede llamar al controlador ODBC para Oracle en cualquier momento, el controlador bloquea cualquier otro subproceso del controlador en la misma conexión hasta que el subproceso original salga del controlador.  
  
 El controlador no se bloquea si hay dos instrucciones en dos conexiones diferentes. Sin embargo, si hay una sola conexión con dos instrucciones, existe la posibilidad de que se bloquee.
