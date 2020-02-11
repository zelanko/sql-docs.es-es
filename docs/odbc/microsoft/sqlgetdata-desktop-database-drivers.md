---
title: SQLGetData (controladores de base de datos de escritorio) | Microsoft Docs
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
ms.openlocfilehash: 086c5381f1801baf919508525c17faab93746ca0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003357"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (controladores de escritorio de la base de datos)
Esta función puede recuperar datos de cualquier columna, tanto si hay columnas enlazadas detrás como si no, independientemente del orden en el que se recuperen las columnas.  
  
> [!NOTE]  
>  \*pcbValue en **SQLGetData** puede devolver dos veces el número de caracteres que realmente esté disponible al enlazar a datos ANSI de más de 510 caracteres en una base de datos Jet 4,0. Los valores de carácter de 510 o menos devolverán el valor de cbValue real.
