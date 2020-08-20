---
description: Errores aritméticos
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
ms.openlocfilehash: 3e2fa142b43f1e96693390f777c90ea6f10705f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500408"
---
# <a name="arithmetic-errors"></a>Errores aritméticos
El controlador ODBC evalúa la cláusula WHERE en una instrucción SELECT cuando captura cada fila. Si una fila contiene un valor que produce un error aritmético, como división por cero o desbordamiento numérico, el controlador devuelve todas las filas, pero devuelve errores para las columnas con errores aritméticos. Sin embargo, al insertar o actualizar, el controlador ODBC deja de insertar o actualizar los datos cuando se encuentra el primer error aritmético.
