---
title: Pruebas de aplicaciones interoperables Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1d43c7aad2501591c497475f6c250ac33712aa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307746"
---
# <a name="testing-interoperable-applications"></a>Probar aplicaciones interoperables
Probar aplicaciones interoperables es, en el mejor de los casos, un negocio que consume mucho tiempo y, en el peor, es imposible porque los nuevos impulsores aparecen continuamente en el mercado. Sin embargo, es posible un grado razonable de prueba. Las aplicaciones con interoperabilidad limitada o baja solo deben probarse con respecto a los controladores que se les garantiza que admiten. Sin embargo, deben ser completamente probados contra estos controladores.  
  
 Las aplicaciones altamente interoperables no se pueden probar prácticamente contra todos los controladores. Lo mejor que la mayoría de los desarrolladores de aplicaciones pueden hacer es probarlos completamente contra un pequeño número de controladores y cursorily contra varios más. Los controladores probados deben incluir los controladores más populares para los DBMS más populares en el mercado de la aplicación; si el mercado cubre todos los DBMS, se deben probar los controladores para los DBMS de escritorio y servidor.  
  
 Uno de los problemas en la prueba de aplicaciones ODBC es el número de componentes implicados: la propia aplicación, el Administrador de controladores, el controlador, el DBMS y posiblemente el software de red o puertas de enlace. Las aplicaciones pueden facilitar el seguimiento de errores mediante la publicación de los mensajes de error devueltos por las funciones ODBC a través de **SQLGetDiagField** y **SQLGetDiagRec**. Estos mensajes identifican el fabricante y el componente en el que se producen errores. Para obtener más información, consulte [Diagnósticos](../../../odbc/reference/develop-app/diagnostics.md).
