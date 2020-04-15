---
title: Creación y terminación de hilos de la página de trabajo de la zona de la Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3536deef604d7dbf645903e7d171a58cd9fec96a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301696"
---
# <a name="creating-and-terminating-threads"></a>Crear y terminar subprocesos
Las aplicaciones multiproceso que usan ODBC deben llamar a las funciones Microsoft® Visual C++® Biblioteca en tiempo de ejecución **_beginthread** y **_endthread** (o **_beginthreadex** y **_endthreadex)** para crear y terminar subprocesos que llamen al Administrador de controladores ODBC. Si las aplicaciones llaman a las funciones de Microsoft Windows NT® **CreateThread** y **EndThread** en su lugar, se producirán pérdidas de memoria porque el Administrador de controladores y algunos controladores ODBC llaman a funciones en tiempo de ejecución de C que no funcionarán en un subproceso creado mediante una llamada a **CreateThread**. Para obtener más información, consulte la documentación de Microsoft Windows®.
