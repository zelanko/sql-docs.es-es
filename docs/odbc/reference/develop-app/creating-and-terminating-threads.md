---
title: Crear y terminar subprocesos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301696"
---
# <a name="creating-and-terminating-threads"></a>Crear y terminar subprocesos
Las aplicaciones multiproceso que usan ODBC deben llamar a las funciones de la biblioteca en tiempo de ejecución de Microsoft® Visual C++® **_beginthread** y **_endthread** (o **_beginthreadex** y **_endthreadex) para**crear y finalizar los subprocesos que llaman al administrador de controladores ODBC. Si las aplicaciones llaman a las funciones de Microsoft Windows NT® **CreateThread** y **EndThread** en su lugar, se producirán pérdidas de memoria porque el administrador de controladores y algunos controladores ODBC llaman a funciones en tiempo de ejecución de C que no funcionarán en un subproceso creado mediante una llamada a **CreateThread**. Para obtener más información, vea la documentación de Microsoft Windows®.
