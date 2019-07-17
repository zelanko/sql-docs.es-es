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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e0880e1746b4b65070fb28bf8d83aadec301aa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138179"
---
# <a name="arithmetic-errors"></a>Errores aritméticos
El controlador ODBC se evalúa como la cláusula WHERE de una instrucción SELECT cuando recupera cada fila. Si una fila contiene un valor que se produce un error aritmético, como desbordamiento numérico o de división por cero, el controlador devuelve todas las filas, pero devuelve errores para las columnas con los errores aritméticos. Al insertar o actualizar, sin embargo, el controlador ODBC deja de inserción o actualización de datos cuando se encuentra el primer error aritmético.
