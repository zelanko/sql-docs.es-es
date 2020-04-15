---
title: Reglas para las conversiones ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c49177d62fffc3b3b5c47a25bf3fb421d7564245
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305091"
---
# <a name="rules-for-conversions"></a>Reglas para conversiones
Las reglas de esta sección se aplican a las conversiones que implican literales numéricos. A los efectos de estas reglas, se definen los siguientes términos:  
  
-   *Asignación de tienda:* Al enviar datos a una columna de tabla en una base de datos. Esto ocurre durante las llamadas a **SQLExecute**, **SQLExecDirect**y **SQLSetPos**. Durante la asignación de almacén, "destino" hace referencia a una columna de base de datos y "origen" hace referencia a los datos de los búferes de aplicación.  
  
-   *Asignación de recuperación:* Al recuperar datos de la base de datos en búferes de aplicación. Esto ocurre durante las llamadas a **SQLFetch**, **SQLGetData**, **SQLFetchScroll**y **SQLSetPos**. Durante la asignación de recuperación, "destino" hace referencia a los búferes de aplicación y "source" hace referencia a la columna de base de datos.  
  
-   *CS:* El valor del origen de caracteres.  
  
-   *NT:* El valor del destino numérico.  
  
-   *NS:* El valor del origen numérico.  
  
-   *CT:* El valor en el destino del carácter.  
  
-   Precisión de un literal numérico exacto: el número de dígitos que contiene.  
  
-   La escala de un literal numérico exacto: el número de dígitos a la derecha del período expresado o implícito.  
  
-   La precisión de un literal numérico aproximado: la precisión de su mantisa.  
  
## <a name="character-source-to-numeric-target"></a>Origen del personaje al objetivo numérico  
 A continuación se muestran las reglas para convertir de un origen de caracteres (CS) a un destino numérico (NT):  
  
1.  Reemplace CS por el valor obtenido eliminando cualquier espacio inicial o final en CS. Si CS no es un *literal numérico*válido, se devuelve SQLSTATE 22018 (valor de carácter no válido para la especificación de conversión).  
  
2.  Reemplace CS por el valor obtenido eliminando los ceros a la izquierda antes del punto decimal, los ceros finales después del punto decimal o ambos.  
  
3.  Convierta CS a NT. Si la conversión da como resultado una pérdida de dígitos significativos, se devuelve SQLSTATE 22003 (valor numérico fuera del intervalo). Si la conversión da como resultado la pérdida de dígitos no significativos, se devuelve SQLSTATE 01S07 (truncamiento fraccionario).  
  
## <a name="numeric-source-to-character-target"></a>Origen numérico al destino del personaje  
 A continuación se muestran las reglas para convertir de un origen numérico (NS) a un destino de carácter (CT):  
  
1.  Deje que LT sea la longitud en caracteres de CT. Para la asignación de recuperación, LT es igual a la longitud del búfer en caracteres menos el número de bytes en el carácter de terminación nula para este juego de caracteres.  
  
2.  Casos:  
  
    -   Si NS es un tipo numérico exacto, deje que YP sea igual a la cadena de caracteres más corta que se ajusta a la definición de *literal numérico exacto* de modo que la escala de YP sea la misma que la escala de NS, y el valor interpretado de YP es el valor absoluto de NS.  
  
    -   Si NS es un tipo numérico aproximado, deje que YP sea una cadena de caracteres de la siguiente manera:  
  
         Caso:  
  
         Si NS es igual a 0, entonces YP es 0.  
  
         Deje que YSN sea la cadena de caracteres más corta que se ajuste a la definición de*literal numérico* exacto y cuyo valor interpretado sea el valor absoluto de NS. Si la longitud de YSN es menor que la (*precisión* + 1) del tipo de datos de NS, deje que YP sea igual a YSN.  
  
         De lo contrario, YP es la cadena de caracteres más corta que se ajusta a la definición de *literal numérico aproximado* cuyo valor interpretado es el valor absoluto de NS y cuya *mantisa* consta de un solo *dígito* que no es '0', seguido de un *punto* y un *entero sin signo.*  
  
3.  Caso:  
  
    -   Si NS es menor que 0, deje que Y sea el resultado de:  
  
         '-' &#124;&#124; YP  
  
         donde '&#124;&#124;' es el operador de concatenación de cadenas.  
  
         De lo contrario, deje Y igual a YP.  
  
4.  Deje que LY sea la longitud en caracteres de Y.  
  
5.  Caso:  
  
    -   Si LY es igual a LT, CT se establece en Y.  
  
    -   Si LY es menor que LT, CT se establece en Y extendido a la derecha por el número adecuado de espacios.  
  
         De lo contrario (LY > LT), copie los primeros caracteres LT de Y en CT.  
  
         Caso:  
  
         Si se trata de una asignación de almacén, devuelva el error SQLSTATE 22001 (datos de cadena, truncados con el botón derecho).  
  
         Si se trata de una asignación de recuperación, devuelva la advertencia SQLSTATE 01004 (datos de cadena, truncados con el botón derecho). Cuando la copia da como resultado la pérdida de dígitos fraccionarios (que no sean ceros finales), se define por el controlador si se produce una de las siguientes situaciones:  
  
         (1) El controlador trunca la cadena en Y a una escala adecuada (que también puede ser cero) y escribe el resultado en CT.  
  
         (2) El controlador redondea la cadena en Y a una escala adecuada (que también puede ser cero) y escribe el resultado en CT.  
  
         (3) El controlador no trunca ni ronda, sino que simplemente copia los primeros caracteres LT de Y en CT.
