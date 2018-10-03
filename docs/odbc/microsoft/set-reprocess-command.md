---
title: CONJUNTO de comandos de volver a procesar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41877986d5d0e8afdfb30841860df360efd26da0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649693"
---
# <a name="set-reprocess-command"></a>CONJUNTO de comandos de volver a procesar
Especifica cuántas horas o durante largos para bloquear un archivo o registro tras un intento infructuoso de bloqueo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>Argumentos  
 PARA *nAttempts*[segundos]  
 Especifica el número de veces o el número de segundos que intentan bloquear un registro o archivo después de intentar un error inicial. El valor predeterminado es 0; el valor máximo es 32.000.  
  
 SEGUNDOS especifica que Visual FoxPro intenta bloquear un archivo o registro para *nAttempts* segundos. Solo está disponible cuando *nAttempts* es mayor que cero.  
  
 Por ejemplo, si *nAttempts* es 30, Visual FoxPro intenta bloquear un registro o archivo hasta 30 veces superior. Si también incluye a establecer volver a procesar y 30 (segundos), Visual FoxPro continuamente intenta bloquear un archivo o registro de hasta 30 segundos.  
  
 Si una rutina ON ERROR está en vigor y si fallan los intentos de un comando para bloquear el registro o archivo, se ejecuta la rutina ON ERROR. Sin embargo, si una función trata el bloqueo, no se ejecuta una rutina ON ERROR y la función devuelve False (. F.).  
  
 Si una rutina ON ERROR no está en vigor, un comando intenta bloquear el registro o archivo y no se puede colocar el bloqueo, se genera un error. Si una función intenta colocar el bloqueo, no se muestra la alerta y la función devuelve False (. F.).  
  
 Si *nAttempts* es 0 (el valor predeterminado) y emitir un comando o una función que intenta bloquear un registro o archivo, Visual FoxPro intenta bloquear el registro o archivo indefinidamente. Si el registro o archivo esté disponible para bloquear mientras espera, se coloca el bloqueo y se borra el mensaje del sistema. Si se intenta una función colocar el bloqueo, la función devuelve True (. T.).  
  
 Si una rutina ON ERROR está en vigor y un comando que está intentando bloquear el registro o archivo, la rutina ON ERROR tiene prioridad sobre los intentos adicionales para bloquear el registro o archivo. Inmediatamente se ejecuta la rutina ON ERROR. Visual FoxPro no realiza bloqueos de archivo o registro adicional y no muestra el mensaje del sistema.  
  
 Si *nAttempts* es 1, Visual FoxPro intenta bloquear el registro o archivo indefinidamente y no se ejecuta una rutina ON ERROR.  
  
 Si se ha colocado un bloqueo de otro usuario en el registro o archivo que está intentando bloquear, debe esperar hasta que el usuario libera el bloqueo.  
  
 EN AUTOMÁTICO  
 Especifica que los intentos de Visual FoxPro bloquear el registro o un archivo indefinidamente. (Conjunto de volver a procesar a -2 es un comando equivalente).  
  
## <a name="remarks"></a>Comentarios  
 El primer intento de bloquear un registro o el archivo no siempre es correcta. Con frecuencia, un registro o el archivo está bloqueado por otro usuario en la red. ESTABLECER REPROCESAR determina si Visual FoxPro hace intentos adicionales para bloquear el registro o archivo cuando el intento inicial es incorrecto. Puede especificar cuántas veces se realizan de intentos adicionales o para los intentos de cuánto se realizan. Una rutina ON ERROR afecta a cómo incorrecta bloqueo se controlan los intentos.
