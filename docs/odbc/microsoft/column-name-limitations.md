---
title: Limitaciones de nombre de columna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a80ed397ae494bc686ef76aaeeef10b61662f19
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301808"
---
# <a name="column-name-limitations"></a>Limitaciones de nombre de columna
Los nombres de columna pueden contener cualquier carácter válido (por ejemplo, espacios en blanco). Si los nombres de columna contienen cualquier carácter excepto letras, números y caracteres de subrayado, el nombre debe estar delimitado escribiéndolo en el back-comillas (').  
  
 Cuando se usa el controlador de Microsoft Access o Microsoft Excel, los nombres de columna se limitan a 64 caracteres y nombres más largos generan un error. Cuando se usa el controlador de Paradox, el nombre de columna máximo es de 25 caracteres. Cuando se usa el controlador de texto, el nombre de columna máximo es de 64 caracteres, y se truncan los nombres más largos.  
  
 Cuando se usa el controlador de dBASE, caracteres con un valor ASCII mayor que 127 se convierten en caracteres de subrayado.  
  
 Cuando se utiliza el controlador de Microsoft Excel, si los nombres de columna están presentes, deben estar en la primera fila. Un nombre que en Microsoft Excel, debe usar el "!" caracteres deben escribirse entre comillas atrás ('). El "!" carácter se convierte en el carácter "$", porque el "!" carácter no es legal en un nombre de ODBC, incluso cuando el nombre está entre comillas atrás. Todos los demás caracteres válidos de Microsoft Excel (excepto el carácter de barra vertical (&#124;)) se puede usar en un nombre de columna, incluidos los espacios. Un identificador delimitado debe usarse para un nombre de columna de Microsoft Excel para que incluya un espacio. Los nombres de columna no especificado se reemplazará con nombres generados por el controlador, por ejemplo, "Col1" para la primera columna.  
  
 El carácter de barra vertical (&#124;) no se puede usar en un nombre de columna, si el nombre está entre comillas atrás o no.  
  
 Cuando se usa el controlador de texto, el controlador proporciona un nombre predeterminado si no se especifica un nombre de columna. Por ejemplo, el controlador llama a la primera columna F1, la segunda columna F2 y así sucesivamente.
