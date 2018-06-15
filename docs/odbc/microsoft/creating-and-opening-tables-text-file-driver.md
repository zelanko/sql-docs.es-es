---
title: Crear y abrir tablas (controlador de archivo de texto) | Documentos de Microsoft
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
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b836fa5144ffb59a155eed150f3372385d808343
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32899630"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Crear y abrir tablas (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, se crea una nueva tabla con el formato especificado en Odbcinst.ini. Si no se especifica, se crean tablas en formato CSVDELIMITED. De forma predeterminada, las columnas de enteros como valor predeterminado de 11 caracteres y columnas de tipo FLOAT predeterminada a 22 caracteres. Columnas de fecha y utilice el formato aaaa-MM-DD. CHAR y columnas LONGCHAR son el ancho especificado en la instrucción CREATE.
