---
title: Crear y abrir tablas (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae13312299f131d1957557db28bbe4db0bf7b4c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280925"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Crear y abrir tablas (controlador de archivo de texto)
Cuando se usa el controlador de texto, se crea una nueva tabla con el formato especificado en Odbcinst. ini. Si no se especifica, las tablas se crean en formato CSVDELIMITED. De forma predeterminada, las columnas de tipo Integer tienen como valor predeterminado 11 caracteres y las columnas FLOAT tienen como valor predeterminado 22 caracteres. Las columnas de fecha usan el formato AAAA-MM-DD. Las columnas CHAR y LONGCHAR son el ancho especificado en la instrucción CREATE.
