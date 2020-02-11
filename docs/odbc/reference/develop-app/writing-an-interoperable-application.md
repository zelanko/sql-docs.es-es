---
title: Escritura de una aplicación interoperable | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f24e50b7f6dd8b129a2777ce1132ec426b7ea182
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078984"
---
# <a name="writing-an-interoperable-application"></a>Escribir una aplicación Interoperable
Cada vez que una aplicación utiliza el mismo código en más de un controlador, ese código debe ser interoperable entre estos controladores. En la mayoría de los casos, se trata de una tarea sencilla. Por ejemplo, el código para capturar filas con un cursor de solo avance es el mismo para todos los controladores. En algunos casos, esto puede ser más difícil. Por ejemplo, el código para construir identificadores para su uso en las instrucciones SQL debe tener en cuenta las convenciones de nomenclatura de mayúsculas y minúsculas de identificadores, y de una parte, dos partes y tres partes.  
  
 En general, el código interoperable debe afrontar problemas de compatibilidad de características y variabilidad de características. La *compatibilidad con características* se refiere a si se admite o no una característica determinada. Por ejemplo, no todos los DBMS admiten transacciones, y el código interoperable debe funcionar correctamente independientemente de la compatibilidad con transacciones. La *variabilidad de características* hace referencia a la variación de la manera en que se admite una característica determinada. Por ejemplo, los nombres de catálogo se colocan al principio de los identificadores en algunos DBMS y al final de los identificadores en otros.  
  
 Las aplicaciones pueden hacer frente a la compatibilidad de características y la variabilidad de características en tiempo de diseño o en tiempo de ejecución. Para tratar con la compatibilidad y la variabilidad de las características en tiempo de diseño, un desarrollador examina los DBMS y los controladores de destino, y se asegura de que el mismo código sea interoperable entre ellos. Por lo general, se trata de la forma en que las aplicaciones con una interoperabilidad baja o limitada abordan estos problemas.  
  
 Por ejemplo, si el desarrollador garantiza que una aplicación vertical solo funcionará con cuatro DBMS determinados y si cada uno de esos DBMS admite transacciones, la aplicación no necesita código para comprobar la compatibilidad con transacciones en tiempo de ejecución. Siempre puede suponer que las transacciones están disponibles debido a la decisión en tiempo de diseño de usar solo cuatro DBMS, cada una de las cuales admite transacciones.  
  
 Para tratar con la compatibilidad y la variabilidad de las características en tiempo de ejecución, la aplicación debe probar las distintas funcionalidades en tiempo de ejecución y actuar en consecuencia. Por lo general, es la forma en que las aplicaciones altamente interoperables abordan estos problemas. En el caso de problemas de compatibilidad de características, esto significa escribir código que hace que la característica sea opcional o escribir código que eMule la característica cuando no está disponible. En el caso de problemas de variabilidad de características, esto significa escribir código que admita todas las variaciones posibles.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Comprobación de compatibilidad con las características y la variabilidad](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Características para vigilar](../../../odbc/reference/develop-app/features-to-watch-for.md)
