---
title: Comando de ANSI SET. | Documentos de Microsoft
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
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2095dc0b30fc2e16d4ce691cc097dcda1614d090
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="set-ansi-command"></a>Comando de ANSI SET.
Determina cómo se realizan las comparaciones entre cadenas de longitudes diferentes con el operador = de comandos SQL de Visual FoxPro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 (Valor predeterminado para el controlador; el valor predeterminado de Visual FoxPro es OFF). Rellena para que la cadena más corta con los espacios en blanco necesarios que tenga una longitud de la cadena igual que más tiempo. Las dos cadenas son, a continuación, en comparación con carácter por carácter para sus longitudes todos. Tenga en cuenta esta comparación:  
  
```  
'Tommy' = 'Tom'  
```  
  
 El resultado es False (. F.) si SET ANSI está activado, porque al relleno, 'Tom' vuelve 'Tom' y las cadenas 'Tom' y 'Juan' no coincide con el carácter por carácter.  
  
 El == (operador) usa este método para realizar comparaciones en comandos SQL de Visual FoxPro.  
  
 OFF  
 Especifica que la cadena más corta no se rellenan con espacios en blanco. Se comparan las dos cadenas carácter por carácter hasta que se llega al final de la cadena más corta. Tenga en cuenta esta comparación:  
  
```  
'Tommy' = 'Tom'  
```  
  
 El resultado es True (. T.) cuando SET ANSI está desactivado, ya que la comparación se detiene después de 'Tom'.  
  
## <a name="remarks"></a>Comentarios  
 SET ANSI determina si la cadena más corta de dos cadenas se rellena con espacios en blanco cuando se realiza una comparación de cadenas SQL. SET ANSI no tiene ningún efecto el operador; == Cuando se usa el operador ==, la cadena más corta siempre se rellena con espacios en blanco para la comparación.  
  
## <a name="string-order"></a>Orden de cadena  
 En los comandos SQL, el orden de izquierda a derecha de las dos cadenas en una comparación es irrelevantswitching una cadena a partir de un lado de la = o == operador a otro no afecta al resultado de la comparación.  
  
## <a name="see-also"></a>Vea también  
 [Seleccione - comando SQL](../../odbc/microsoft/select-sql-command.md)   
 [Comando exacto de conjunto](../../odbc/microsoft/set-exact-command.md)

