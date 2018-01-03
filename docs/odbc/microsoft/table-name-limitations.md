---
title: Limitaciones de nombre de tabla | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b001db50394ea1e9cf7c52d9519294fb66dbcdfc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="table-name-limitations"></a>Limitaciones de nombre de tabla
Los nombres de tabla pueden contener cualquier carácter válido (por ejemplo, espacios en blanco). Si los nombres de tabla contienen cualquier carácter excepto letras, números y caracteres de subrayado, el nombre debe estar delimitado, incluya entre comillas atrás (').  
  
 Cuando se utiliza el controlador de Microsoft Excel y un nombre de tabla no está calificado por una referencia de base de datos, la base de datos predeterminada está implícita. Si un nombre en Microsoft Excel incluye el "!" carácter, automáticamente se traducirá en el carácter "$" en su lugar.  
  
 El nombre de la tabla de Microsoft Excel que hace referencia a \<filename > es compatible con Microsoft Excel 3.0 y 4.0 archivos. El nombre de la tabla de Microsoft Excel que hace referencia a \<libro-name > es compatible con archivos de Microsoft Excel 5.0, 7.0 ó 97.  
  
 Cuando se utiliza el controlador dBASE, caracteres con un valor ASCII mayor que 127 se convierten en caracteres de subrayado.  
  
 Cuando se utiliza el controlador de Microsoft Access, el nombre de tabla se limita a 64 caracteres.  
  
 Cuando se utiliza el controlador de Microsoft Excel 3.0 o 4.0, Paradox o texto dBASE, palabras clave especiales MS-DOS CON, AUX, LPT1 y LPT2 no debe usarse como nombres de tabla.
