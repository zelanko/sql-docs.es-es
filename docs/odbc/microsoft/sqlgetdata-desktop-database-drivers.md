---
title: SQLGetData (controladores de base de datos de escritorio) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e091bf31e034eaabb9c87931bc6b128f5bdeba84
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (controladores de escritorio de la base de datos)
Esta función puede recuperar datos de cualquier columna, si no hay columnas enlazadas después de él e independientemente del orden en el que se recuperan las columnas.  
  
> [!NOTE]  
>  \*pcbValue en **SQLGetData** puede devolver dos veces la cantidad de caracteres realmente disponibles cuando se enlazan a datos ANSI más de 510 caracteres en una base de datos de Jet 4.0. Valores de caracteres de 510 o menos devolverá el cbValue real.
