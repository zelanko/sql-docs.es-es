---
title: Limitaciones de nombre de columna ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41d973afdac360af114da41620997cad23a2c740
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281385"
---
# <a name="column-name-limitations"></a>Limitaciones de nombre de columna
Los nombres de columna pueden contener caracteres válidos (por ejemplo, espacios). Si los nombres de columna contienen caracteres excepto letras, números y guiones bajos, el nombre debe delimitarse encerrándolo entre comillas (').  
  
 Cuando se usa el controlador de Microsoft Access o Microsoft Excel, los nombres de columna están limitados a 64 caracteres y los nombres más largos generan un error. Cuando se utiliza el controlador Paradox, el nombre máximo de columna es de 25 caracteres. Cuando se utiliza el controlador de texto, el nombre máximo de columna es de 64 caracteres y los nombres más largos se truncan.  
  
 Cuando se utiliza el controlador dBASE, los caracteres con un valor ASCII mayor que 127 se convierten en guiones bajos.  
  
 Cuando se usa el controlador de Microsoft Excel, si hay nombres de columna, deben estar en la primera fila. Un nombre que en Microsoft Excel usaría el carácter "!" debe incluirse entre comillas inversas ('). El carácter "!" se convierte en el carácter "$", porque el carácter "!" no es legal en un nombre ODBC, incluso cuando el nombre está entre comillas. Todos los demás caracteres válidos de Microsoft Excel (excepto el carácter de tubería (&#124;)) se pueden utilizar en un nombre de columna, incluidos los espacios. Se debe usar un identificador delimitado para que un nombre de columna de Microsoft Excel incluya un espacio. Los nombres de columna no especificados se reemplazarán por nombres generados por el controlador, por ejemplo, "Col1" para la primera columna.  
  
 El carácter de tubería (&#124;) no se puede utilizar en un nombre de columna, independientemente de si el nombre está entre comillas o no.  
  
 Cuando se utiliza el controlador de texto, el controlador proporciona un nombre predeterminado si no se especifica un nombre de columna. Por ejemplo, el controlador llama a la primera columna F1, la segunda columna F2, etc.
