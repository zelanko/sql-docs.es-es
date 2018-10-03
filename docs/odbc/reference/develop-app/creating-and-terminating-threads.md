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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722383"
---
# <a name="creating-and-terminating-threads"></a>Crear y terminar subprocesos
Aplicaciones multiproceso que utilizan ODBC deben llamar a las funciones de biblioteca de tiempo de ejecución de Microsoft® Visual C++® **_beginthread** y **_endthread** (o **_beginthreadex** y **_endthreadex**) para crear y terminar subprocesos que llaman a Administrador de controladores ODBC. Si las aplicaciones llaman a las funciones de Microsoft Windows NT® **CreateThread** y **EndThread** en su lugar, funciones de memoria pérdidas se producen porque el Administrador de controladores y algunos controladores ODBC llaman a tiempo de ejecución de C no funcionará en un subproceso creado por una llamada a **CreateThread**. Para obtener más información, consulte la documentación de Microsoft Windows®.
