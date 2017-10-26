---
title: Crear y abrir tablas (controlador de archivo de texto) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41190a0a3eabda2f73c8f6046a64b7b7db929fa1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="creating-and-opening-tables-text-file-driver"></a>Crear y abrir tablas (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, se crea una nueva tabla con el formato especificado en Odbcinst.ini. Si no se especifica, se crean tablas en formato CSVDELIMITED. De forma predeterminada, las columnas de enteros como valor predeterminado de 11 caracteres y columnas de tipo FLOAT predeterminada a 22 caracteres. Columnas de fecha y utilice el formato aaaa-MM-DD. CHAR y columnas LONGCHAR son el ancho especificado en la instrucción CREATE.

