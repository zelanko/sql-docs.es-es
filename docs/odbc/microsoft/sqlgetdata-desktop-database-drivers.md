---
title: SQLGetData (controladores de base de datos de escritorio) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2bd9088fa327783019d0b025ab4daaacd951852b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (controladores de escritorio de la base de datos)
Esta función puede recuperar datos de cualquier columna, si no hay columnas enlazadas después de él e independientemente del orden en el que se recuperan las columnas.  
  
> [!NOTE]  
>  \*pcbValue en **SQLGetData** puede devolver dos veces la cantidad de caracteres realmente disponibles cuando se enlazan a datos ANSI más de 510 caracteres en una base de datos de Jet 4.0. Valores de caracteres de 510 o menos devolverá el cbValue real.
