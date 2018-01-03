---
title: Crear y terminar subprocesos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 62950dba2174baac8e3bc34c60f268e07304fa5a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="creating-and-terminating-threads"></a>Crear y terminar subprocesos
Aplicaciones multiproceso que utilicen ODBC deben llamar a las funciones de biblioteca de tiempo de ejecución de Microsoft® Visual C++® **_beginthread** y **_endthread** (o **_beginthreadex** y **_endthreadex**) para crear y terminar subprocesos que llaman a Administrador de controladores ODBC. Si las aplicaciones llaman a las funciones de Microsoft Windows NT® **CreateThread** y **EndThread** en su lugar, funciones de memoria pérdidas se producen porque el Administrador de controladores y algunos controladores ODBC llaman a tiempo de ejecución de C no funcionará en un subproceso creado mediante una llamada a **CreateThread**. Para obtener más información, consulte la documentación de Microsoft Windows®.
