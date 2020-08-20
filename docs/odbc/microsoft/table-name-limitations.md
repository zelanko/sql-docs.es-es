---
description: Limitaciones de nombre de tabla
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef1395ab9e112e045fb90dc6f06a83b96bc48697
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471477"
---
# <a name="table-name-limitations"></a>Limitaciones de nombre de tabla
Los nombres de tabla pueden contener cualquier carácter válido (por ejemplo, espacios). Si los nombres de tabla contienen caracteres excepto letras, números y caracteres de subrayado, el nombre debe delimitarse mediante la inclusión de comillas dobles (').  
  
 Cuando se utiliza el controlador de Microsoft Excel, y un nombre de tabla no está calificado por una referencia de base de datos, la base de datos predeterminada es implícita. Si un nombre de Microsoft Excel incluye el carácter "!", se traducirá automáticamente al carácter "$".  
  
 El nombre de tabla de Microsoft Excel al que hace referencia \<filename> es compatible con los archivos de Microsoft excel 3,0 y 4,0. El nombre de tabla de Microsoft Excel al que hace referencia \<workbook-name> es compatible con archivos de Microsoft excel 5,0, 7,0 o 97.  
  
 Cuando se usa el controlador dBASE, los caracteres con un valor ASCII superior a 127 se convierten en caracteres de subrayado.  
  
 Cuando se usa el controlador de Microsoft Access, el nombre de la tabla está limitado a 64 caracteres.  
  
 Cuando se usa el controlador dBASE, Microsoft Excel 3,0 o 4,0, Paradox o Text, no se deben usar como nombres de tabla las palabras clave especiales de MS-DOS con, AUX, LPT1 y LPT2.
