---
title: Limitaciones de nombre de columna | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5e2fb7cf9f54177ce357058e51e541b6a442379
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="column-name-limitations"></a>Limitaciones de nombre de columna
Nombres de columna pueden contener cualquier carácter válido (por ejemplo, espacios en blanco). Si los nombres de columna contienen los caracteres excepto letras, números y caracteres de subrayado, el nombre debe estar delimitado, incluya entre comillas atrás (').  
  
 Cuando se utiliza el controlador de Microsoft Access o Microsoft Excel, los nombres de columna están limitados a 64 caracteres y nombres más largos generan un error. Cuando se utiliza el controlador de Paradox, el nombre de columna máximo es de 25 caracteres. Cuando se utiliza el controlador de texto, el nombre de columna máximo es de 64 caracteres, y se truncan nombres más largos.  
  
 Cuando se utiliza el controlador dBASE, caracteres con un valor ASCII mayor que 127 se convierten en caracteres de subrayado.  
  
 Cuando se utiliza el controlador de Microsoft Excel, si no hay nombres de columna, deben estar en la primera fila. Un nombre que en Microsoft Excel, debe usar el "!" caracteres deben incluirse entre comillas atrás ('). El "!" carácter se convierte en el carácter "$", porque el "!" carácter no es válido en un nombre ODBC, incluso cuando el nombre está entre comillas atrás. Todos los demás caracteres válidos de Microsoft Excel (excepto el carácter de canalización (& #124 ;)) puede utilizarse en un nombre de columna, incluidos los espacios. Un identificador delimitado debe utilizarse para un nombre de columna de Microsoft Excel para incluir un espacio. Nombres de columna especificado se reemplazará con nombres generados por el controlador, por ejemplo, "Col1" para la primera columna.  
  
 El carácter de canalización (&#124;) no se puede usar en un nombre de columna, si el nombre está entre comillas atrás o no.  
  
 Cuando se utiliza el controlador de texto, el controlador proporciona un nombre predeterminado si no se especifica un nombre de columna. Por ejemplo, el controlador llama a la primera columna F1, la segunda columna F2 y así sucesivamente.

