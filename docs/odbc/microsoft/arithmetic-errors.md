---
title: "Los errores aritméticos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0a24a87c814c51bcf3270298b56b5ffec01fa29
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="arithmetic-errors"></a>Errores aritméticos
El controlador ODBC se evalúa como la cláusula WHERE de una instrucción SELECT como recupera cada fila. Si una fila contiene un valor que se produce un error aritmético, como un desbordamiento numérico o de división por cero, el controlador devuelve todas las filas, pero devuelve errores para las columnas con errores aritméticos. Al insertar o actualizar, sin embargo, el controlador ODBC detiene insertar o actualizar datos cuando se encuentra el primer error aritmético.
