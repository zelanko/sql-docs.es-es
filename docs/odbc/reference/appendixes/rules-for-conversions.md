---
title: Reglas para conversiones | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3ecee500204303dfcbcd8e179b9cb9cb0a94bae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032918"
---
# <a name="rules-for-conversions"></a>Reglas para conversiones
Las reglas en esta sección se aplican las conversiones que involucran literales numéricos. Para los fines de estas reglas, se definen los términos siguientes:  
  
-   *Asignación de Store:* Al enviar datos a una columna de tabla en una base de datos. Esto sucede durante las llamadas a **SQLExecute**, **SQLExecDirect**, y **SQLSetPos**. Durante la asignación de la tienda, "target" hace referencia a una columna de base de datos y "origen" hace referencia a los datos en búferes de la aplicación.  
  
-   *Asignación de recuperación:* Al recuperar datos de la base de datos en búferes de la aplicación. Esto sucede durante las llamadas a **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, y **SQLSetPos**. Durante la asignación de recuperación, "target" se refiere a los búferes de la aplicación y "origen" hace referencia a la columna de base de datos.  
  
-   *CS:* El valor en el origen del carácter.  
  
-   *NT:* El valor en el destino numérico.  
  
-   *NS:* El valor en el origen numérico.  
  
-   *CT:* El valor en el destino de caracteres.  
  
-   Precisión de un literal numérico exacto: el número de dígitos que lo contiene.  
  
-   La escala de un literal numérico exacto: el número de dígitos a la derecha del período expresa o implícita.  
  
-   La precisión de un literal numérico aproximado: la precisión de la mantisa.  
  
## <a name="character-source-to-numeric-target"></a>Carácter de origen a destino numérico  
 A continuación figuran las reglas de conversión de un origen de caracteres (CS) a un destino numérico (NT):  
  
1.  Reemplace el valor obtenido al quitar los espacios iniciales o finales en CS CS. Si no es válido el CS *literales numéricos*, se devuelve SQLSTATE 22018 (valor de carácter no válido para especificación cast).  
  
2.  Reemplace el valor obtenido mediante la eliminación de ceros delante del separador decimal, finales ceros después del separador decimal, o ambos CS.  
  
3.  Convertir CS en NT. Si la conversión produce una pérdida de dígitos significativos, se devuelve SQLSTATE 22003 (valor numérico fuera del intervalo). Si la conversión tiene como resultado la pérdida de dígitos no significativos, SQLSTATE 01S07 (truncamiento fraccionario) se devuelve.  
  
## <a name="numeric-source-to-character-target"></a>Origen numérico a caracteres de destino  
 A continuación figuran las reglas de conversión de un origen numérico (NS) a un destino de caracteres (CT):  
  
1.  Se denominará LT la longitud en caracteres de CT. Para la asignación de recuperación, LT es igual que la longitud del búfer en caracteres, menos el número de bytes en el carácter de terminación null para este juego de caracteres.  
  
2.  Casos:  
  
    -   Si NS es un tipo numérico exacto, a continuación, dejar que es igual a la cadena más corta de caracteres que se ajusta a la definición de *literal numérico exacto* tal que la escala de YP es igual que la escala de NS, y el valor de YP interpretado es el valor absoluto de NS.  
  
    -   Si NS es un tipo numérico aproximado, a continuación, se denominará YP una cadena de caracteres como sigue:  
  
         Caso:  
  
         Si es igual a 0 NS, YP es 0.  
  
         Se denominará YSN la cadena más corta de caracteres que se ajusta a la definición exacta-*literales numéricos* y cuyo valor interpretado es el valor absoluto de NS. Si la longitud de YSN es menor que (*precisión* + 1) del tipo de datos de NS, a continuación, dejar que YP igual YSN.  
  
         En caso contrario, YP es la cadena más corta de caracteres que se ajusta a la definición de *literal numérico aproximado* cuyo valor interpretado es el valor absoluto de NS y cuyo *mantisa* consta de un solo *dígitos* que es no '0', seguido por un *período* y un *entero sin signo*.  
  
3.  Caso:  
  
    -   Si NS es menor que 0, a continuación, se denominará Y el resultado de:  
  
         '-' &AMP;#124; &AMP;#124; YP  
  
         donde '&#124;&#124;' es el operador de concatenación de cadenas.  
  
         En caso contrario, deje que Y es igual a YP.  
  
4.  Permita que LY sea la longitud en caracteres de Y.  
  
5.  Caso:  
  
    -   Si LY es igual a LT, CT esté establecido en Y.  
  
    -   Si LY es menor que LT, a continuación, CT se establece en Y extendido a la derecha por el número adecuado de espacios.  
  
         En caso contrario (LY > LT), copie los primeros caracteres LT de Y CT.  
  
         Caso:  
  
         Si se trata de una asignación de la tienda, devolverá el error SQLSTATE 22001 (datos de cadena, truncados a la derecha).  
  
         Si se trata de una asignación de recuperación, devolver la advertencia SQLSTATE 01004 (datos de cadena, truncados a la derecha). Cuando la copia da como resultado la pérdida de dígitos fraccionarios (excepto los ceros finales), está definido por el controlador si se produce uno de los siguientes:  
  
         (1) el controlador trunca la cadena en Y a escala adecuada (que puede ser cero también) y escribe el resultado en CT.  
  
         (2) el controlador redondea la cadena en Y a escala adecuada (que puede ser cero también) y escribe el resultado en CT.  
  
         (3) el controlador ni trunca ni se redondea, pero sólo los primeros caracteres LT de Y copia en CT.
