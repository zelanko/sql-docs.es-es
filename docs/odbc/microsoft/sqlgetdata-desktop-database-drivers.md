---
title: SQLGetData (Controladores de base de datos de escritorio) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b102d8435831d45aad3c2049581513e0493de9a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304126"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (controladores de escritorio de la base de datos)
Esta función puede recuperar datos de cualquier columna, independientemente de si hay columnas enlazadas después de ella e independientemente del orden en el que se recuperan las columnas.  
  
> [!NOTE]  
>  \*pcbValue en **SQLGetData** puede devolver el doble de caracteres que realmente disponible al enlazar a datos ANSI de más de 510 caracteres en una base de datos Jet 4.0. Los valores de carácter de 510 o menos devolverán el cbValue real.
