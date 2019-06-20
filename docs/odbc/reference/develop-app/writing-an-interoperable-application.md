---
title: Escribir una aplicación Interoperable | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8e559eab5787a64b6bdf0850147d7d9128fc435c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208579"
---
# <a name="writing-an-interoperable-application"></a>Escribir una aplicación Interoperable
Cada vez que una aplicación utiliza el mismo código con más de un controlador, que el código debe ser interoperable entre esos controladores. En la mayoría de los casos, esto es una tarea fácil. Por ejemplo, el código para capturar las filas con un cursor de solo avance es el mismo para todos los controladores. En algunos casos, esto puede ser más difícil. Por ejemplo, el código para construir los identificadores para su uso en instrucciones SQL debe considerar el caso del identificador entrecomillado y las convenciones de nomenclatura de tres partes, dos partes y una parte.  
  
 En general, debe hacer frente código interoperable con problemas de compatibilidad de las características y la variabilidad de característica. *Compatibilidad con las características* se refiere a si o no se admite una característica determinada. Por ejemplo, no todos los DBMS admiten las transacciones y código interoperable debe funcionar correctamente con independencia de la compatibilidad con transacciones. *Característica variabilidad* hace referencia a la variación de la manera en que se admite una característica determinada. Por ejemplo, los nombres de catálogo se colocan al principio de los identificadores en algunos de los DBMS y al final de los identificadores en otras.  
  
 Pueden tratar las aplicaciones con compatibilidad con las características y la variabilidad de característica en tiempo de diseño o en tiempo de ejecución. Para tratar con compatibilidad con las características y variabilidad en tiempo de diseño, un desarrollador examina el DBMS de destino y los controladores y se asegura que el mismo código serán interoperable entre ellos. Esto suele ser la manera en que las aplicaciones con interoperabilidad baja o limitado tratan estos problemas.  
  
 Por ejemplo, si el programador garantiza que una aplicación vertical solo funcionarán con cuatro DBMS determinados y cada uno de los DBMS admite transacciones, la aplicación no necesita código para comprobar la compatibilidad con transacciones en tiempo de ejecución. Puede suponer siempre las transacciones están disponibles debido a la decisión de tiempo de diseño para usar solo cuatro DBMS, cada uno de los cuales admite transacciones.  
  
 Para tratar con compatibilidad con las características y variabilidad en tiempo de ejecución, la aplicación debe probar para distintas capacidades en tiempo de ejecución y actuar en consecuencia. Esto suele ser la manera en que las aplicaciones muy interoperables tratan estos problemas. Para problemas de compatibilidad de característica, esto significa escribir código que hace que el código de función opcional o escribir que emula la característica cuando no esté disponible. Para los problemas de la variabilidad de característica, esto significa escribir código que es compatible con todas las variaciones posibles.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Comprobación de compatibilidad con las características y la variabilidad](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Características para vigilar](../../../odbc/reference/develop-app/features-to-watch-for.md)
