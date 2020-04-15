---
title: Cumplimiento de SQL-92 (SQL-92 Compliance) Microsoft Docs
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
ms.openlocfilehash: 9ac0ae5873e545afb8fcac9dd003c984b1ed303a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300705"
---
# <a name="sql-92-compliance"></a>Cumplimiento de normas de SQL-92
Los controladores de base de datos de escritorio ODBC y el motor de Microsoft Jet subyacente no son compatibles con SQL-92. Admiten muchas características que se han definido en SQL-92. Algunas características admitidas en el controlador no se admiten en SQL-92. Para obtener más información, consulte la Guía del programador de *Microsoft Jet Database Engine*. Las siguientes son las principales diferencias entre los dos:  
  
-   El SQL utilizado por los controladores de base de datos de escritorio admite expresiones más eficaces que las especificadas por SQL-92.  
  
-   Se aplican reglas diferentes al predicado BETWEEN.  
  
-   El SQL utilizado por los controladores de base de datos de escritorio y ANSI SQL admite diferentes palabras clave.  
  
 Microsoft Jet SQL no admite las siguientes características de SQL-92:  
  
-   Instrucciones de seguridad, como GRANT y LOCK.  
  
-   DISTINCT con referencias de función agregada.  
  
 Las siguientes características son mejoras en el SQL utilizado por los controladores de base de datos de escritorio que no se especifican en SQL-92:  
  
-   La instrucción TRANSFORM que proporciona compatibilidad con consultas de tabla de referencias cruzadas.  
  
-   Funciones de agregado adicionales (**StDev** y **VarP**).  
  
> [!NOTE]  
>  Los controladores de base de datos de escritorio admiten la sintaxis ANSI estándar para % (porcentaje) y _ (subrayado), no * (asterisco) y ? (signo de interrogación).
