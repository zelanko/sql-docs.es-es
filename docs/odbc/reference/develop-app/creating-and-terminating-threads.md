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
manager: craigg
ms.openlocfilehash: e9d6d15c449d88043e844addd12ac10a98d5c4a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470873"
---
# <a name="creating-and-terminating-threads"></a>Crear y terminar subprocesos
Aplicaciones multiproceso que utilizan ODBC deben llamar a la Visual de Microsoft® C++® funciones de biblioteca en tiempo de ejecución **_beginthread** y **_endthread** (o **_beginthreadex**y **_endthreadex**) para crear y terminar subprocesos que llaman a Administrador de controladores ODBC. Si las aplicaciones llaman a las funciones de Microsoft Windows NT® **CreateThread** y **EndThread** en su lugar, funciones de memoria pérdidas se producen porque el Administrador de controladores y algunos controladores ODBC llaman a tiempo de ejecución de C no funcionará en un subproceso creado por una llamada a **CreateThread**. Para obtener más información, consulte la documentación de Microsoft Windows®.
