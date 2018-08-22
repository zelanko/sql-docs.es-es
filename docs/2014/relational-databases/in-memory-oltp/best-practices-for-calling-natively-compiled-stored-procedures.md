---
title: Procedimientos recomendados para llamar a procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
caps.latest.revision: 8
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3c867721b0e7868a57f4a76108e2b9029dc22172
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395981"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>Prácticas recomendadas para llamar a un procedimiento almacenado compilado de forma nativa
  Los procedimientos almacenados compilados de forma nativa:  
  
-   Se suelen usar en componentes esenciales para el rendimiento de una aplicación.  
  
-   Se ejecutan con frecuencia.  
  
-   Se espera que sean muy rápidos.  
  
 La ventaja de rendimiento que supone emplear un procedimiento almacenado compilado de forma nativa aumenta con el número de filas y la cantidad de lógica que procesa el procedimiento. Por ejemplo, un procedimiento almacenado compilado de forma nativa tendrá mejor rendimiento si usa uno o varios de los elementos siguientes:  
  
-   Agregación.  
  
-   Combinaciones de bucles anidados.  
  
-   Operaciones de inserción, actualización y eliminación de varias instrucciones.  
  
-   Expresiones complejas.  
  
-   Lógica de procedimientos, como instrucciones condicionales y bucles.  
  
 Si solo necesita procesar una única fila, el uso de un procedimiento almacenado compilado de forma nativa quizás no proporcione ventajas de rendimiento.  
  
 Para evitar que el servidor tenga que asignar nombres de parámetro y convertir tipos:  
  
-   Haga corresponder los tipos de parámetros pasados al procedimiento con los tipos de la definición del procedimiento.  
  
-   Use parámetros ordinales (anónimos) cuando llame a procedimientos almacenados compilados de forma nativa. Para que la ejecución sea más eficaz, no utilice parámetros con nombre.  
  
 El uso de parámetros con nombre (ineficaces) con procedimientos almacenados compilados de forma nativa se puede detectar con el XEvent `hekaton_slow_parameter_passing`, con `reason=named_parameters`.  
  
 De forma similar, puede detectar el uso de tipos no coincidentes a través del mismo XEvent `hekaton_slow_parameter_passing`, con `reason=parameter_conversion`.  
  
 Puesto que necesitará implementar lógica de reintentos cuando use tablas optimizadas para memoria (en varios escenarios), y como necesitará evitar ciertas limitaciones de la característica, puede ser conveniente crear un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado por el contenedor. Para obtener un ejemplo, vea [Guidelines for Retry Logic para las transacciones en tablas optimizadas para memoria](memory-optimized-tables.md).  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)  
  
  
