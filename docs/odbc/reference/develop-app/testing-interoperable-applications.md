---
title: Probar aplicaciones interoperables | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 59f6f5a37e65c802c8d51a1f56a40380f054e39b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114089"
---
# <a name="testing-interoperable-applications"></a>Probar aplicaciones interoperables
En el mejor lleva un tiempo probar aplicaciones interoperables empresariales y en el peor caso posible dado que los nuevos controladores que continuamente aparecen en el mercado. Sin embargo, un nivel razonable de las pruebas es posible. Solo se necesitan probar aplicaciones con interoperabilidad baja o limitada en aquellos controladores que se garantiza la compatibilidad. Sin embargo, debe ser probados completamente contra estos controladores.  
  
 No se pueden probar aplicaciones muy interoperables prácticamente en todos los controladores. Lo mejor que pueden hacer la mayoría de los desarrolladores de aplicaciones es probarlas completamente con respecto a un pequeño número de controladores y cursorily varios más. Controladores probados deben incluir los controladores más populares para el DBMS más populares en el mercado de la aplicación. Si el mercado cubre todos los DBMS, se deben probar controladores para escritorios y servidores DBMS.  
  
 Uno de los problemas en las pruebas de las aplicaciones ODBC es el número de componentes que intervienen: la propia aplicación, el Administrador de controladores, el controlador, el DBMS y posiblemente el software de red o puertas de enlace. Las aplicaciones pueden hacer más fácil realizar un seguimiento de errores mediante el registro de los mensajes de error devueltos por las funciones ODBC a través de **SQLGetDiagField** y **SQLGetDiagRec**. Estos mensajes identifican el fabricante y el componente en el que se producen errores. Para obtener más información, consulte [diagnósticos](../../../odbc/reference/develop-app/diagnostics.md).
