---
description: Cumplimiento de normas de SQL-92
title: Cumplimiento de SQL-92 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d978b236c45d442732cd3602c3fbbb6d16dfd8f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483438"
---
# <a name="sql-92-compliance"></a>Cumplimiento de normas de SQL-92
Los controladores de base de datos de escritorio ODBC y el motor de Microsoft Jet subyacente no son compatibles con SQL-92. Admiten muchas características que se han definido en SQL-92. Algunas características admitidas en el controlador no se admiten en SQL-92. Para obtener más información, vea la *Guía del programador de Microsoft Jet motor de base de datos*. Las siguientes son las principales diferencias entre los dos:  
  
-   El SQL que usan los controladores de base de datos de escritorio admite expresiones más eficaces que las especificadas por SQL-92.  
  
-   Se aplican reglas diferentes al predicado BETWEEN.  
  
-   El SQL que usan los controladores de base de datos de escritorio y ANSI SQL admite diferentes palabras clave.  
  
 Las siguientes características de SQL-92 no son compatibles con Microsoft Jet SQL:  
  
-   Instrucciones de seguridad, como GRANT y LOCK.  
  
-   DISTINCt con referencias a funciones de agregado.  
  
 Las siguientes características son mejoras en el SQL que usan los controladores de base de datos de escritorio que no se especifican en SQL-92:  
  
-   La instrucción TRANSFORM que proporciona compatibilidad con las consultas de referencias cruzadas.  
  
-   Funciones de agregado adicionales (**stdev** y **VarP**).  
  
> [!NOTE]  
>  Los controladores de base de datos de escritorio admiten la sintaxis ANSI estándar para% (porcentaje) y _ (carácter de subrayado), no * (asterisco) y? (signo de interrogación).
