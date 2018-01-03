---
title: "Aplicaciones genéricas | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 471cceb31dfec36cde45185d3d472aba3100b4da
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="generic-applications"></a>Aplicaciones genéricas
Aplicaciones genéricas a veces, realizan una tarea codificado de forma rígida, como una hoja de cálculo de recuperar datos de una base de datos. También pueden realizar diversas tareas definidas por el usuario, como una aplicación de consultas genérico que permite al usuario escribir y ejecutar una instrucción SQL. ¿Qué aplicaciones genéricas tienen en común es que debe trabajar con una variedad de diferentes DBMS y que el programador no conoce de antemano cuál será estos DBMS.  
  
 Por lo tanto, las aplicaciones genéricas deben ser muy interoperable. El programador debe realizar muchas opciones, compensando la interoperabilidad de características y debe escribir código que espera controladores para admitir una amplia gama de funcionalidad. Mientras las aplicaciones genéricas podrían corregirse para trabajar con DBMS conocidos, rara vez contienen código específico del controlador o específicos del DBMS.
