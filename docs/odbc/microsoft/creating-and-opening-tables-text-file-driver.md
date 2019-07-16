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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b36c02d772682088a799cfca66f5bbf3e169a67f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096543"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Crear y abrir tablas (controlador de archivo de texto)
Cuando se usa el controlador de texto, se crea una nueva tabla con el formato especificado en Odbcinst.ini. Si no se especifica, se crean tablas en formato CSVDELIMITED. De forma predeterminada, las columnas de enteros predeterminado a 11 caracteres y columnas de punto flotante como valor predeterminado 22 caracteres. Columnas de fecha y utilice el formato aaaa-MM-DD. CHAR y columnas LONGCHAR son el ancho especificado en la instrucción CREATE.
