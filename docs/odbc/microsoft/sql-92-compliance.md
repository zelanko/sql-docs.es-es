---
title: Cumplimiento de normas de SQL-92 | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a925896250a307c7d256232377ec6d9325c8db77
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sql-92-compliance"></a>Cumplimiento de normas de SQL-92
Los controladores de base de datos de escritorio de ODBC y el motor subyacente de Microsoft Jet no son compatibles con SQL-92. Admiten muchas características que se han definido en SQL-92. Algunas características admitidas en el controlador no se admiten en SQL-92. Para obtener más información, consulte el *Guía del programador del motor de base de datos Jet de Microsoft*. Éstas son las principales diferencias entre los dos:  
  
-   El código SQL que se usan los controladores de base de datos de escritorio admite expresiones más eficaces que las especificadas por SQL-92.  
  
-   Se aplican reglas diferentes para el predicado BETWEEN.  
  
-   El SQL utilizado por los controladores de base de datos de escritorio y ANSI SQL admite palabras clave diferentes.  
  
 No se admiten las siguientes características de SQL-92 por Microsoft Jet SQL:  
  
-   Instrucciones de seguridad, como GRANT y bloqueo.  
  
-   DISTINCT con referencias de función de agregado.  
  
 Las siguientes características son mejoras en el código SQL que se usan los controladores de base de datos de escritorio que no se especifican por SQL-92:  
  
-   La instrucción TRANSFORM proporcionar soporte para las consultas de tabla de referencias cruzadas.  
  
-   Otras funciones de agregado (**StDev** y **VarP**).  
  
> [!NOTE]  
>  ¿Los controladores de base de datos de escritorio admiten la sintaxis de ANSI estándar para % (porcentaje) y _ (carácter de subrayado), no * (asterisco) y? (signo de interrogación).

