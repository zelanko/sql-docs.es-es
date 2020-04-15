---
title: Errores aritméticos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab1b472540d1978a6e7a06d94da7542cc641e999
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299905"
---
# <a name="arithmetic-errors"></a>Errores aritméticos
El controlador ODBC evalúa la cláusula WHERE en una instrucción SELECT a medida que recupera cada fila. Si una fila contiene un valor que provoca un error aritmético, como dividir por cero o desbordamiento numérico, el controlador devuelve todas las filas, pero devuelve errores para columnas con errores aritméticos. Sin embargo, al insertar o actualizar, el controlador ODBC deja de insertar o actualizar datos cuando se encuentra el primer error aritmético.
