---
title: Comando SET REPROCESS (Comando SET REPROCESS) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a7eb5fd19ca538c4f25077926567011ae133e54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300835"
---
# <a name="set-reprocess-command"></a>CONJUNTO de comandos de volver a procesar
Especifica cuántas veces o durante cuánto tiempo se debe bloquear un archivo o registro después de un intento de bloqueo fallido.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>Argumentos  
 TO *nAttempts*[SECONDS]  
 Especifica el número de veces o el número de segundos para intentar bloquear un registro o archivo después de un intento fallido inicial. El valor predeterminado es 0; el valor máximo es 32.000.  
  
 SECONDS especifica que Visual FoxPro intenta bloquear un archivo o registro durante *nAttempts* segundos. Solo está disponible cuando *nAttempts* es mayor que cero.  
  
 Por ejemplo, si *nAttempts* es 30, Visual FoxPro intenta bloquear un registro o archivo hasta 30 veces. Si también incluye SECONDS (SET REPROCESS TO 30 SECONDS), Visual FoxPro intenta bloquear continuamente un registro o archivo durante un máximo de 30 segundos.  
  
 Si una rutina ON ERROR está en vigor y si los intentos de un comando para bloquear el registro o archivo no tienen éxito, se ejecuta la rutina ON ERROR. Sin embargo, si una función intenta el bloqueo, no se ejecuta una rutina ON ERROR y la función devuelve False (. F.).  
  
 Si una rutina ON ERROR no está en vigor, un comando intenta bloquear el registro o archivo y no se puede colocar el bloqueo, se genera un error. Si una función intenta colocar el bloqueo, la alerta no se muestra y la función devuelve False (. F.).  
  
 Si *nAttempts* es 0 (el valor predeterminado) y emite un comando o función que intenta bloquear un registro o archivo, Visual FoxPro intenta bloquear el registro o archivo indefinidamente. Si el registro o archivo está disponible para el bloqueo mientras espera, se coloca el bloqueo y se borra el mensaje del sistema. Si una función intenta colocar el bloqueo, la función devuelve True (. T.).  
  
 Si una rutina ON ERROR está en vigor y un comando está intentando bloquear el registro o archivo, la rutina ON ERROR tiene prioridad sobre los intentos adicionales de bloquear el registro o archivo. La rutina ON ERROR se ejecuta inmediatamente. Visual FoxPro no intenta bloqueos de registro sin archivos o registros adicionales y no muestra el mensaje del sistema.  
  
 Si *nAttempts* es 1, Visual FoxPro intenta bloquear el registro o archivo indefinidamente y no se ejecuta una rutina ON ERROR.  
  
 Si otro usuario ha colocado un bloqueo en el registro o archivo que está intentando bloquear, debe esperar hasta que el usuario libere el bloqueo.  
  
 A AUTOMÁTICO  
 Especifica que Visual FoxPro intenta bloquear el registro o el archivo indefinidamente. (SET REPROCESS TO -2 es un comando equivalente.)  
  
## <a name="remarks"></a>Observaciones  
 El primer intento de bloquear un registro o archivo no siempre es correcto. Con frecuencia, otro usuario de la red bloquea un registro o archivo. SET REPROCESS determina si Visual FoxPro realiza intentos adicionales para bloquear el registro o el archivo cuando el intento inicial no se realiza correctamente. Puede especificar cuántas veces se realizan intentos adicionales o durante cuánto tiempo se realizan los intentos. Una rutina ON ERROR afecta a cómo se gestionan los intentos de bloqueo fallidos.
