---
title: "Pr&#225;cticas recomendadas para llamar a un procedimiento almacenado compilado de forma nativa | Microsoft Docs"
ms.custom: ""
ms.date: "03/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# Pr&#225;cticas recomendadas para llamar a un procedimiento almacenado compilado de forma nativa
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
  
 El uso de parámetros con nombre (ineficaces) con procedimientos almacenados compilados de forma nativa se puede detectar con el XEvent **hekaton_slow_parameter_passing**, con **reason=named_parameters**.  
  
 De forma similar, puede detectar el uso de tipos no coincidentes a través del mismo XEvent **hekaton_slow_parameter_passing**, con **reason=parameter_conversion**.  
  
 Puesto que necesitará implementar lógica de reintentos cuando use tablas con optimización para memoria (en varios escenarios), y como necesitará evitar ciertas limitaciones de la característica, puede ser conveniente crear un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado por el contenedor. Para obtener un ejemplo, vea [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md) (Transacciones con tablas con optimización para memoria).  
  
## Vea también  
 [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  