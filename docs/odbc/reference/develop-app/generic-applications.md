---
title: Aplicaciones genéricas ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607676d5370f02ee1d39196bff9261bc897521ee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305556"
---
# <a name="generic-applications"></a>Aplicaciones genéricas
Las aplicaciones genéricas a veces realizan una tarea codificada de forma rígida, como una hoja de cálculo que recupera datos de una base de datos. También pueden realizar una variedad de tareas definidas por el usuario, como una aplicación de consulta genérica que permite al usuario escribir y ejecutar una instrucción SQL. Lo que las aplicaciones genéricas tienen en común es que deben trabajar con una variedad de DBMS diferentes y que el desarrollador no sabe de antemano cuáles serán estos DBMS.  
  
 Por lo tanto, las aplicaciones genéricas deben ser altamente interoperables. El desarrollador debe tomar muchas decisiones, comerciar con la interoperabilidad de las características y debe escribir código que espere que los controladores admitan una amplia gama de funciones. Aunque las aplicaciones genéricas se pueden ajustar para trabajar con DBMS populares, rara vez contienen código específico del controlador o específico de DBMS.
