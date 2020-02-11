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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b97f29ad06c4ed961f3cee571b0ca7b8d9c0b774
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002082"
---
# <a name="creating-and-terminating-threads"></a>Crear y terminar subprocesos
Las aplicaciones multiproceso que usan ODBC deben llamar a las funciones de la biblioteca en tiempo de ejecución de Microsoft® Visual C++® **_beginthread** y **_endthread** (o **_beginthreadex** y **_endthreadex) para**crear y finalizar los subprocesos que llaman al administrador de controladores ODBC. Si las aplicaciones llaman a las funciones de Microsoft Windows NT® **CreateThread** y **EndThread** en su lugar, se producirán pérdidas de memoria porque el administrador de controladores y algunos controladores ODBC llaman a funciones en tiempo de ejecución de C que no funcionarán en un subproceso creado mediante una llamada a **CreateThread**. Para obtener más información, vea la documentación de Microsoft Windows®.
