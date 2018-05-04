---
title: Reglas para las conversiones | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38d4fa50d82cf81b47dc50c44410d9e47ca3dfe5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="rules-for-conversions"></a>Reglas para conversiones
Las reglas de esta sección se aplican para las conversiones que involucran literales numéricos. Para los fines de estas reglas, se definen los términos siguientes:  
  
-   *Almacenar asignación:* al enviar datos en una columna de tabla en una base de datos. Esto sucede durante las llamadas a **SQLExecute**, **SQLExecDirect**, y **SQLSetPos**. Durante la asignación de almacén de "destino" hace referencia a una columna de base de datos y "origen" hace referencia a los datos en búferes de la aplicación.  
  
-   *Asignación de recuperación:* al recuperar datos de la base de datos en búferes de la aplicación. Esto sucede durante las llamadas a **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, y **SQLSetPos**. Durante la asignación de recuperación, "destino" hace referencia a los búferes de la aplicación y "origen" hace referencia a la columna de base de datos.  
  
-   *CS:* el valor en el origen del carácter.  
  
-   *NT:* el valor en el destino numérico.  
  
-   *NS:* el valor de origen numéricos.  
  
-   *CT:* el valor en el destino de carácter.  
  
-   Precisión de un literal numérico exacto: el número de dígitos que lo contiene.  
  
-   La escala de un literal numérico exacto: el número de dígitos a la derecha del período expresa o implícita.  
  
-   La precisión de un literal numérico aproximado: la precisión de la mantisa.  
  
## <a name="character-source-to-numeric-target"></a>Caracteres de origen a destino numérico  
 A continuación figuran las reglas para convertir de un origen de carácter (CS) a un destino numérico (NT):  
  
1.  Reemplace CS por el valor obtenido mediante la eliminación de los espacios iniciales o finales en CS. Si no es válido CS *literal numérico*, se devuelve SQLSTATE 22018 (valor de carácter no válido para especificación cast).  
  
2.  Reemplace CS por el valor obtenido mediante la eliminación de ceros a la izquierda antes del punto decimal, finales ceros después del punto decimal, o ambos.  
  
3.  Convertir CS en NT. Si la conversión tiene como resultado una pérdida de dígitos significativos, se devuelve SQLSTATE 22003 (valor numérico fuera del intervalo). Si la conversión tiene como resultado la pérdida de dígitos no significativos, SQLSTATE 01S07 (truncamiento fraccionario) se devuelve.  
  
## <a name="numeric-source-to-character-target"></a>Origen numérico a caracteres de destino  
 A continuación figuran las reglas para convertir de un origen numéricos (NS) a un destino de carácter (CT):  
  
1.  Se denominará LT la longitud en caracteres de CT. Para la asignación de recuperación, LT es igual que la longitud del búfer en caracteres menos el número de bytes en el carácter de terminación null de este juego de caracteres.  
  
2.  Casos:  
  
    -   Si Servicios de notificación es un tipo numérico exacto, a continuación, dejar YP igual a la cadena más corta de caracteres que se ajuste a la definición de *literal numérico exacto* forma que la escala de NIS es el mismo que la escala de NS, y el valor interpretado de NIS es el valor absoluto de NS.  
  
    -   Si Servicios de notificación es un tipo numérico aproximado, a continuación, se denominará YP una cadena de caracteres como sigue:  
  
         Caso:  
  
         Si es igual a 0 NS, YP es 0.  
  
         Se denominará YSN la cadena de caracteres más corta que se ajuste a la definición de exacta -*literal numérico* y cuyo valor interpretado es el valor absoluto de NS. Si la longitud de YSN es menor que (*precisión* + 1) del tipo de datos de NS, a continuación, dejar YP YSN es igual.  
  
         En caso contrario, YP es la cadena más corta de caracteres que se ajuste a la definición de *literal numérico aproximado* cuyo valor interpretado es el valor absoluto de NS y cuyo *mantisa* consta de un solo *dígitos* que es no '0', seguido por un *período* y un *entero sin signo*.  
  
3.  Caso:  
  
    -   Si NS es menor que 0, a continuación, dejar Y ser el resultado de:  
  
         '-' &AMP;#124; &AMP;#124; YP  
  
         donde '&#124;&#124;' es el operador de concatenación de cadenas.  
  
         De lo contrario, deje que Y YP es igual.  
  
4.  Supongamos que LY es la longitud en caracteres de Y.  
  
5.  Caso:  
  
    -   Si LY es igual a LT, CT esté establecido en Y.  
  
    -   Si LY es menor que LT, a continuación, CT se establece en Y extendido a la derecha por el número adecuado de espacios.  
  
         En caso contrario (LY > LT), copie los primeros caracteres LT de Y en CT.  
  
         Caso:  
  
         Si se trata de una asignación de almacén, devolverá el error SQLSTATE 22001 (datos de cadena, truncado a la derecha).  
  
         Si se trata de asignación de recuperación, devolver la advertencia SQLSTATE 01004 (datos de cadena, truncado a la derecha). Cuando la copia da como resultado la pérdida de dígitos fraccionarios (distintos de los ceros finales), está definido por el controlador si se produce una de las siguientes acciones:  
  
         (1) el controlador trunca la cadena en Y a una escala adecuada (que puede ser cero también) y escribe el resultado en CT.  
  
         (2) el controlador redondea la cadena en Y a una escala adecuada (que puede ser cero también) y escribe el resultado en CT.  
  
         (3) el controlador no trunca ni redondea, pero sólo copia los primeros caracteres LT de Y en CT.
