---
title: "Escribir una aplicación Interoperable | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bab5be84b66571f7ca361a3b158921330c00007f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="writing-an-interoperable-application"></a>Escribir una aplicación Interoperable
Cada vez que una aplicación usa el mismo código con más de un controlador, que el código debe ser interoperable entre los controladores. En la mayoría de los casos, esto es una tarea sencilla. Por ejemplo, el código para capturar las filas con un cursor de sólo avance es el mismo para todos los controladores. En algunos casos, esto puede ser más difícil. Por ejemplo, el código para crear identificadores para su uso en instrucciones SQL debe tener en cuenta el caso del identificador, comillas y las convenciones de nomenclatura de tres partes, dos partes y una parte.  
  
 En general, debe abordar el código interoperable con problemas de compatibilidad con las características y la variabilidad de característica. *Compatibilidad con las características* se refiere a si o no se admite una característica determinada. Por ejemplo, no todos los DBMS admiten las transacciones y código interoperable debe funcionar correctamente con independencia de la compatibilidad con transacciones. *Característica variabilidad* hace referencia a la variación de la manera en que se admite una característica determinada. Por ejemplo, los nombres de catálogo se colocan al principio de identificadores en algunos de los DBMS y al final de los identificadores en otras.  
  
 Las aplicaciones pueden tratar con compatibilidad con las características y la variabilidad de característica en tiempo de diseño o en tiempo de ejecución. Para tratar con compatibilidad con las características y la variabilidad en tiempo de diseño, un desarrollador examina el DBMS de destino y los controladores y se asegura de que el mismo código serán interoperable entre ellos. Por lo general, suele ser la manera en que las aplicaciones con interoperabilidad baja o limitada ocuparse de estos problemas.  
  
 Por ejemplo, si el desarrollador garantiza que una aplicación vertical solo funcionarán con cuatro DBMS determinados y cada uno de los DBMS admite las transacciones, la aplicación no necesita código para comprobar la compatibilidad de transacción en tiempo de ejecución. Siempre puede asumir las transacciones están disponibles debido a la decisión de tiempo de diseño para usar solo cuatro DBMS, cada uno de los cuales admite transacciones.  
  
 Para tratar con compatibilidad con las características y la variabilidad en tiempo de ejecución, la aplicación debe comprobar distintas funcionalidades en tiempo de ejecución y actuar en consecuencia. Por lo general, suele ser la manera en que aplicaciones muy interoperables abordar estos problemas. Para los problemas de compatibilidad de característica, esto significa que escribir código que hace que el característica opcional o escribir código que emula la característica cuando no está disponible. Para los problemas de la variabilidad de característica, esto significa que escribir código que es compatible con todas las variantes posibles.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Comprobación de compatibilidad con las características y la variabilidad](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Características para vigilar](../../../odbc/reference/develop-app/features-to-watch-for.md)

