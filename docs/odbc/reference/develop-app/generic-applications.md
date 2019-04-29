---
title: Aplicaciones genéricas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59110f66c512845ff5ce1f2f246c05c63fa755b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061503"
---
# <a name="generic-applications"></a>Aplicaciones genéricas
Aplicaciones genéricas en ocasiones, realizan una tarea codificado de forma rígida, como una hoja de cálculo de recuperación de datos de una base de datos. También es posible que realizan diversas tareas definidas por el usuario, como una aplicación de consultas genérico que permite al usuario escribir y ejecutar una instrucción SQL. ¿Qué aplicaciones genéricas tienen en común es que deben trabajar con una variedad de diferentes DBMS y que el desarrollador no conoce de antemano cuál será estos DBMS.  
  
 Por lo tanto, deben ser muy interoperable aplicaciones genéricas. El desarrollador debe realizar numerosas opciones, compensando la interoperabilidad de características y debe escribir código que espera que los controladores para admitir una amplia gama de funcionalidad. Mientras las aplicaciones genéricas se podrían optimizar para trabajar con DBMS conocidos, rara vez contienen código específico del controlador o específicos para DBMS.
