---
title: 'Prácticas recomendadas: procedimientos almacenados compilados de forma nativa'
description: Conozca los procedimientos recomendados que se aplican en relación con los procedimientos almacenados compilados de forma nativa; estos normalmente se usan en partes de una aplicación en las que el rendimiento es crítico.
ms.custom: seo-dt-2019
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 053cd5f7aebf3b84de1bf08104b13aa30488704b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537721"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>Prácticas recomendadas para llamar a un procedimiento almacenado compilado de forma nativa
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
  
 Se pueden detectar deficiencias en parámetros con procedimientos almacenados compilados de forma nativa mediante XEvent **natively_compiled_proc_slow_parameter_passing**:
 - Tipos no coincidentes: **reason=parameter_conversion**
 - Parámetros con nombre: **reason=named_parameters**
 - Valores predeterminados: **reason=default** 
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
