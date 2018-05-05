---
title: Los errores aritméticos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 867de0b8982b22f9f9574c334226bccc01798065
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="arithmetic-errors"></a>Errores aritméticos
El controlador ODBC se evalúa como la cláusula WHERE de una instrucción SELECT como recupera cada fila. Si una fila contiene un valor que se produce un error aritmético, como un desbordamiento numérico o de división por cero, el controlador devuelve todas las filas, pero devuelve errores para las columnas con errores aritméticos. Al insertar o actualizar, sin embargo, el controlador ODBC detiene insertar o actualizar datos cuando se encuentra el primer error aritmético.
