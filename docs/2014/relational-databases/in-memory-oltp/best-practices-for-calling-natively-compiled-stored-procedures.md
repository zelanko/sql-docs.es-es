---
title: Procedimientos recomendados para llamar a procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 39f88ef6c0b39bb51e4c1ba54388b37e04983b00
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050333"
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
  
 Asimismo, puede detectar el uso de tipos no coincidentes a través del mismo XEvent `hekaton_slow_parameter_passing`, con `reason=parameter_conversion`.  
  
 Puesto que necesitará implementar lógica de reintentos cuando use tablas optimizadas para memoria (en varios escenarios), y como necesitará evitar ciertas limitaciones de la característica, puede ser conveniente crear un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado por el contenedor. Para obtener un ejemplo, vea [instrucciones para la lógica de reintento para las transacciones en tablas optimizadas para memoria](memory-optimized-tables.md).  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)  
  
  
