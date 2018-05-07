---
title: Crear y terminar subprocesos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6568dd1109dc417cad0e5f4ad3d973ae5aaa497a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="creating-and-terminating-threads"></a>Crear y terminar subprocesos
Aplicaciones multiproceso que utilicen ODBC deben llamar a las funciones de biblioteca de tiempo de ejecución de Microsoft® Visual C++® **_beginthread** y **_endthread** (o **_beginthreadex** y **_endthreadex**) para crear y terminar subprocesos que llaman a Administrador de controladores ODBC. Si las aplicaciones llaman a las funciones de Microsoft Windows NT® **CreateThread** y **EndThread** en su lugar, funciones de memoria pérdidas se producen porque el Administrador de controladores y algunos controladores ODBC llaman a tiempo de ejecución de C no funcionará en un subproceso creado mediante una llamada a **CreateThread**. Para obtener más información, consulte la documentación de Microsoft Windows®.
