---
description: Probar aplicaciones interoperables
title: Prueba de aplicaciones interoperables | Microsoft Docs
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
ms.openlocfilehash: feebbe5914e9da1e414f5c77a1a69bc0a6e0e7b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487528"
---
# <a name="testing-interoperable-applications"></a>Probar aplicaciones interoperables
Probar las aplicaciones interoperables es el mejor proceso de negocio y, en el peor de los tiempos, no es posible porque los nuevos controladores aparecen continuamente en el mercado. Sin embargo, es posible un grado razonable de pruebas. Las aplicaciones con una interoperabilidad limitada o baja solo deben probarse con los controladores que se garantiza que admitan. Sin embargo, se deben probar por completo en estos controladores.  
  
 Las aplicaciones altamente interoperables no se pueden probar prácticamente con todos los controladores. Lo mejor que la mayoría de los desarrolladores de aplicaciones pueden hacer es probarlos completamente con un pequeño número de controladores y, de manera más rápida, con respecto a varios. Los controladores probados deben incluir los controladores más populares para los DBMS más populares del mercado de la aplicación; Si el mercado cubre todos los DBMS, se deben probar los controladores para los DBMS de servidor y de escritorio.  
  
 Uno de los problemas de la prueba de aplicaciones ODBC es el número de componentes implicados: la propia aplicación, el administrador de controladores, el controlador, el DBMS y, posiblemente, software de red o puertas de enlace. Las aplicaciones pueden facilitar el seguimiento de los errores mediante la publicación de los mensajes de error devueltos por las funciones ODBC a través de **SQLGetDiagField** y **SQLGetDiagRec**. Estos mensajes identifican el fabricante y el componente en el que se producen errores. Para obtener más información, consulte [diagnósticos](../../../odbc/reference/develop-app/diagnostics.md).
