---
title: Esquema de la versión del controlador (Driver Version Scheme) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 864a8bd892315b060fc6fcf42dbe69dfea61ae59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303456"
---
# <a name="driver-version-scheme"></a>Esquema de la versión de controlador
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 En la tabla siguiente se enumeran todas las versiones publicadas del controlador ODBC de Microsoft para Oracle.  
  
|Versión del controlador|Número de compilación|Historial de disponibilidad|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 y Visual Basic 5.0, Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 y MDAC 1.5a|  
|2.0 actualizado|2.73.7283.01|IIS 4.0|  
|2.0 actualizado|2.73.7283.03|MDAC 1.5b y 1.5c|  
|2.0 actualizado|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 y MDAC 2.0|  
|2.5 actualizado|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 La compilación 2.00.6235 (versión 1) fue la primera versión del controlador ODBC de Microsoft para Oracle. Después del lanzamiento de la primera versión, se adoptó una nueva convención de nomenclatura.  
  
 Por ejemplo, 2.73.7283.03 se puede dividir en los siguientes componentes distintos:  
  
-   2 - El número de versión.  
  
-   73 - La versión de Oracle Server para la que se diseñó el controlador.  
  
-   7283.03 - El número de compilación del controlador.  
  
> [!NOTE]  
>  Con la versión 2.573.2973, la convención de nomenclatura ha dado lugar a cierta confusión de que 2.573 es una versión anterior a 2.73, pero cada sección del número de compilación debe considerarse individualmente. El número 573 es más grande que 73, por lo que es una versión más reciente. Además, "2.5" indica el número de versión del controlador.
