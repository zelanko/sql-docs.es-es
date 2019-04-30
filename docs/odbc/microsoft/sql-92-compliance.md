---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf6d8d056c1658a924de4b108d3c0d025e8a58f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313397"
---
# <a name="sql-92-compliance"></a>Cumplimiento de normas de SQL-92
Los controladores de base de datos ODBC Desktop y el motor subyacente de Microsoft Jet no son compatibles con SQL-92. Admiten muchas características que se han definido en SQL-92. Algunas características admitidas en el controlador no se admiten en SQL-92. Para obtener más información, consulte el *Guía del programador del motor de base de datos Jet de Microsoft*. Los siguientes son las principales diferencias entre los dos:  
  
-   La usan los controladores de base de datos de escritorio SQL admite expresiones más eficaces que los especificados por SQL-92.  
  
-   Se aplican reglas diferentes con el predicado BETWEEN.  
  
-   El SQL utilizado por los controladores de base de datos de escritorio y ANSI SQL es compatible con palabras clave diferentes.  
  
 SQL de Microsoft Jet no admite las siguientes características de SQL-92:  
  
-   Instrucciones de seguridad, como GRANT y bloqueo.  
  
-   DISTINCT con referencias de función de agregado.  
  
 Las siguientes características son mejoras en el SQL que usan los controladores de base de datos de escritorio que no se especifican mediante SQL-92:  
  
-   La instrucción de transformación que proporciona compatibilidad con consultas de referencias cruzadas.  
  
-   Otras funciones de agregado (**StDev** y **VarP**).  
  
> [!NOTE]  
>  ¿Los controladores de base de datos de escritorio admiten la sintaxis de ANSI estándar para % (porcentaje) y _ (carácter de subrayado), no * (asterisco) y? (signo de interrogación).
