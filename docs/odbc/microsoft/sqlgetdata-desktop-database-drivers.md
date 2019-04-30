---
title: SQLGetData (controladores de escritorio de la base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f362d725f8b734ab9ecdbdc79c268af08a495b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313139"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (controladores de escritorio de la base de datos)
Esta función puede recuperar datos de cualquier columna, si hay columnas enlazadas después de él e independientemente del orden en que se recuperan las columnas.  
  
> [!NOTE]  
>  \*pcbValue en **SQLGetData** puede devolver dos veces más caracteres que realmente disponible al enlazar a datos ANSI más de 510 caracteres en una base de datos de Jet 4.0. Los valores de caracteres de 510 o menos devolverá el cbValue real.
