---
title: Escribir una aplicación interoperable ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 553e718e0759e47701e7f8c04561693358d5dc52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289087"
---
# <a name="writing-an-interoperable-application"></a>Escribir una aplicación Interoperable
Cada vez que una aplicación usa el mismo código en más de un controlador, ese código debe ser interoperable entre esos controladores. En la mayoría de los casos, esta es una tarea fácil. Por ejemplo, el código para capturar filas con un cursor de solo avance es el mismo para todos los controladores. En algunos casos, esto puede ser más difícil. Por ejemplo, el código para construir identificadores para su uso en instrucciones SQL debe tener en cuenta las convenciones de nomenclatura de una parte, dos partes y tres partes.  
  
 En general, el código interoperable debe hacer frente a los problemas de compatibilidad con características y variabilidad de características. *La compatibilidad con características* se refiere a si se admite o no una característica determinada. Por ejemplo, no todos los DBMS admiten transacciones y el código interoperable debe funcionar correctamente independientemente de la compatibilidad con transacciones. *La variabilidad* de las características se refiere a la variación en la forma en que se admite una característica determinada. Por ejemplo, los nombres de catálogo se colocan al principio de los identificadores en algunos DBMS y al final de los identificadores de otros.  
  
 Las aplicaciones pueden lidiar con la compatibilidad con características y la variabilidad de las características en tiempo de diseño o en tiempo de ejecución. Para hacer frente a la compatibilidad con características y la variabilidad en tiempo de diseño, un desarrollador examina los DBMS y controladores de destino y se asegura de que el mismo código sea interoperable entre ellos. Esta es generalmente la forma en que las aplicaciones con interoperabilidad baja o limitada se ocupan de estos problemas.  
  
 Por ejemplo, si el desarrollador garantiza que una aplicación vertical funcionará solo con cuatro DBMS concretos y si cada uno de esos DBMS admite transacciones, la aplicación no necesita código para comprobar la compatibilidad con transacciones en tiempo de ejecución. Siempre puede suponer que las transacciones están disponibles debido a la decisión en tiempo de diseño de usar solo cuatro DBMS, cada uno de los cuales admite transacciones.  
  
 Para hacer frente a la compatibilidad con características y la variabilidad en tiempo de ejecución, la aplicación debe probar diferentes capacidades en tiempo de ejecución y actuar en consecuencia. Esta es generalmente la forma en que las aplicaciones altamente interoperables liesten con estos problemas. Para problemas de compatibilidad con características, esto significa escribir código que hace que la característica sea opcional o escribir código que emula la característica cuando no está disponible. Para problemas de variabilidad de características, esto significa escribir código que admita todas las variaciones posibles.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Comprobación de compatibilidad con las características y la variabilidad](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Características para vigilar](../../../odbc/reference/develop-app/features-to-watch-for.md)
