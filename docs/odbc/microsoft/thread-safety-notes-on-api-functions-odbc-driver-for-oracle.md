---
title: Notas de la seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d1faa7dfd8873b8c11cda5cb3e67d5408c35474
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633220"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Notas de seguridad para subprocesos en las funciones de API (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle es segura para subprocesos; Sin embargo, Oracle permite varias instrucciones simultáneas en una sola conexión. El controlador aplica esta restricción. En otras palabras, en las aplicaciones multiproceso, aunque puede llamar cualquier subproceso en el controlador ODBC para Oracle en cualquier momento, el controlador bloquea ningún otro subproceso desde el controlador en la misma conexión hasta que el subproceso original deja el controlador.  
  
 El controlador no se bloquea si hay dos instrucciones en dos conexiones diferentes. Sin embargo, si hay una conexión única con dos instrucciones, es posible para el bloqueo.
