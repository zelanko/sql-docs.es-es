---
title: Errores aritméticos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299905"
---
# <a name="arithmetic-errors"></a>Errores aritméticos
El controlador ODBC evalúa la cláusula WHERE en una instrucción SELECT cuando captura cada fila. Si una fila contiene un valor que produce un error aritmético, como división por cero o desbordamiento numérico, el controlador devuelve todas las filas, pero devuelve errores para las columnas con errores aritméticos. Sin embargo, al insertar o actualizar, el controlador ODBC deja de insertar o actualizar los datos cuando se encuentra el primer error aritmético.
