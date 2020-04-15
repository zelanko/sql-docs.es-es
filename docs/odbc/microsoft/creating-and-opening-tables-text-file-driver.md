---
title: Creación y apertura de tablas (controlador de archivo de texto) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280925"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Crear y abrir tablas (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, se crea una nueva tabla con el formato especificado en Odbcinst.ini. Si no se especifica, las tablas se crean en formato CSVDELIMITED. De forma predeterminada, las columnas INTEGER tienen un valor predeterminado de 11 caracteres y las columnas FLOAT tienen un valor predeterminado de 22 caracteres. Las columnas DATE utilizan el formato AAAA-MM-DD. Las columnas CHAR y LONGCHAR son el ancho especificado en la instrucción CREATE.
