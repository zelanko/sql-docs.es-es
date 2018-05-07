---
title: Probar aplicaciones interoperables | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3025c0ae41e6c677917975efa2742ef4154ce45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="testing-interoperable-applications"></a>Probar aplicaciones interoperables
Probar aplicaciones interoperables en el mejor es una que consumen muchos recursos empresariales y en el peor imposible dado que los nuevos controladores continuamente aparecen en el mercado. Sin embargo, un nivel razonable de pruebas es posible. Solo se necesitan probar las aplicaciones con interoperabilidad baja o limitada en aquellos controladores que se garantiza la compatibilidad. Sin embargo, debe ser totalmente probados con estos controladores.  
  
 No se puede probar aplicaciones muy interoperables prácticamente en todos los controladores. Es lo mejor que pueden realizar la mayoría de los desarrolladores de aplicaciones probarlas completamente con un pequeño número de controladores y cursorily con muchas más. Controladores probados deben incluir los controladores más populares para el DBMS más populares de mercado de la aplicación; Si el mercado cubre todos los DBMS, deberán probarse controladores para DBMS de escritorio y servidores.  
  
 Uno de los problemas en las pruebas de las aplicaciones ODBC es el número de componentes que intervienen: la propia aplicación, el Administrador de controladores, el controlador, el DBMS y posiblemente el software de red o puertas de enlace. Las aplicaciones pueden resulte más fácil realizar un seguimiento de errores mediante el registro de los mensajes de error devueltos por las funciones ODBC a través de **SQLGetDiagField** y **SQLGetDiagRec**. Estos mensajes identifican el fabricante y el componente en el que se producen errores. Para obtener más información, consulte [diagnósticos](../../../odbc/reference/develop-app/diagnostics.md).
