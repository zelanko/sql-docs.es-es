---
title: Comandos con comandos COMPUTE intermedios con parámetros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1675e80522feb0c0b2a46a89dfa6e3bba182198
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851649"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>Comandos de proceso de comandos con parámetros con intermedias
Una forma con parámetros típica comandos APPEND tiene una cláusula que crea un elemento primario **Recordset** con un comando de consulta y otra cláusula que crea un elemento secundario **Recordset** con un comando de consulta con parámetros: es decir, un comando que contiene un marcador de posición de parámetro (un signo de interrogación "?"). El resultado en forma de **Recordset** tiene dos niveles, en el que el elemento primario ocupa el nivel superior y el elemento secundario ocupa el nivel inferior.  
  
 La cláusula que crea el elemento secundario **Recordset** puede ahora ser un número arbitrario de forma anidada comandos COMPUTE, donde el comando más profundamente anidado contiene la consulta con parámetros. El resultado en forma de **Recordset** tiene varios niveles, en el que el elemento primario ocupa el nivel superior, el elemento secundario que ocupa el nivel inferior y un número arbitrario de **Recordset**s generados por el comandos Shape COMPUTE ocupan los niveles intermedios.  
  
 El uso típico de esta característica consiste en llamar a la función de agregado y las capacidades de agrupamiento de shapeCOMPUTE comandos para crear intermedia **Recordset** objetos con información analítica sobre el elemento secundario **conjunto de registros** . Además, puesto que es un comando de forma con parámetros, se accede cada vez que una columna de capítulo del elemento primario, un nuevo elemento secundario **Recordset** se pueden recuperar. Dado que se derivan de los niveles intermedios del elemento secundario, también se volverá a calcular.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)
