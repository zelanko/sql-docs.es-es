---
title: Los errores aritméticos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f63a3c7dd14301fc77a2b4ec1565744ac5015d93
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="arithmetic-errors"></a>Errores aritméticos
El controlador ODBC se evalúa como la cláusula WHERE de una instrucción SELECT como recupera cada fila. Si una fila contiene un valor que se produce un error aritmético, como un desbordamiento numérico o de división por cero, el controlador devuelve todas las filas, pero devuelve errores para las columnas con errores aritméticos. Al insertar o actualizar, sin embargo, el controlador ODBC detiene insertar o actualizar datos cuando se encuentra el primer error aritmético.
