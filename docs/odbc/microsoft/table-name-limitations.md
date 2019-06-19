---
title: Limitaciones de nombre de tabla | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31c1703bc03a2881e7b9b96989b8949cc81aba7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63226345"
---
# <a name="table-name-limitations"></a>Limitaciones de nombre de tabla
Los nombres de tabla pueden contener cualquier carácter válido (por ejemplo, espacios en blanco). Si los nombres de tabla contienen cualquier carácter excepto letras, números y caracteres de subrayado, el nombre debe estar delimitado escribiéndolo en el back-comillas (').  
  
 Cuando se usa el controlador de Microsoft Excel y un nombre de tabla no se califica mediante una referencia de base de datos, la base de datos predeterminada está implícita. Si un nombre en Microsoft Excel incluye el "!", carácter, automáticamente se traducirá en el carácter "$" en su lugar.  
  
 El nombre de la tabla de Microsoft Excel que hace referencia a \<filename > es compatible con Microsoft Excel 3.0 y 4.0 archivos. El nombre de la tabla de Microsoft Excel que hace referencia a \<libro-name > es compatible con archivos de Microsoft Excel 97, 7.0 o 5.0.  
  
 Cuando se usa el controlador de dBASE, caracteres con un valor ASCII mayor que 127 se convierten en caracteres de subrayado.  
  
 Cuando se usa el controlador de Microsoft Access, el nombre de tabla está limitado a 64 caracteres.  
  
 Cuando se usa el controlador de Microsoft Excel 3.0 o 4.0, texto o Paradox, dBASE, palabras clave especiales MS-DOS CON, AUX, LPT1 y LPT2 no deben usarse como nombres de tabla.
