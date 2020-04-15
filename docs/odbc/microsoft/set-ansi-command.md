---
title: Comando SET ANSI ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97269642b4147b966fdd71003f5f81ebe7905282
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300915"
---
# <a name="set-ansi-command"></a>Comando de ANSI SET
Determina cómo se realizan las comparaciones entre cadenas de diferentes longitudes con el operador .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ACTIVAR  
 (Predeterminado para el controlador; el valor predeterminado para Visual FoxPro es OFF.) Rellena la cadena más corta con los espacios en blanco necesarios para que sea igual a la longitud de la cadena más larga. A continuación, se comparan las dos cadenas carácter por carácter para todas sus longitudes. Considere esta comparación:  
  
```  
'Tommy' = 'Tom'  
```  
  
 El resultado es False (. F.) si SET ANSI está activado, porque cuando se rellena, 'Tom' se convierte en 'Tom' y las cuerdas 'Tom' y 'Tommy' no coinciden con el carácter para el carácter.  
  
 Para las comparaciones en los comandos SQL de Visual FoxPro, se utiliza este método para las comparaciones.  
  
 Apagado  
 Especifica que la cadena más corta no se rellena con espacios en blanco. Las dos cadenas se comparan carácter para carácter hasta que se alcanza el final de la cadena más corta. Considere esta comparación:  
  
```  
'Tommy' = 'Tom'  
```  
  
 El resultado es True (. T.) cuando SET ANSI está desactivado, porque la comparación se detiene después de 'Tom'.  
  
## <a name="remarks"></a>Observaciones  
 SET ANSI determina si el más corto de dos cadenas se rellena con espacios en blanco cuando se realiza una comparación de cadenas SQL. SET ANSI no tiene ningún efecto en el operador de la clase; cuando se utiliza el operador de la cadena más corta, la cadena más corta siempre se rellena con espacios en blanco para la comparación.  
  
## <a name="string-order"></a>Orden de cuerda  
 En los comandos SQL, el orden de izquierda a derecha de las dos cadenas en una comparación es irrelevante cambiar una cadena de un lado del operador de .  
  
## <a name="see-also"></a>Consulte también  
 [SELECT - Comando SQL](../../odbc/microsoft/select-sql-command.md)   
 [Comando exacto de conjunto](../../odbc/microsoft/set-exact-command.md)
