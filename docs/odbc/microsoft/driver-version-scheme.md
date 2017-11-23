---
title: "Esquema de la versión de controlador | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 35ee21329cabca4e160112887f8c746ad8f44b82
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="driver-version-scheme"></a>Esquema de la versión de controlador
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 En la tabla siguiente se enumera todas las versiones publicadas de Microsoft ODBC Driver for Oracle.  
  
|Versión del controlador|Número de compilación|Historial de disponibilidad|  
|--------------------|------------------|--------------------------|  
|1,0|2.00.6235|Visual C++ 4.2 y Visual Basic 5.0, edición Enterprise|  
|2,0|2.73.7269|Visual Studio 97 y MDAC 1,5 a|  
|2.0 actualizado|2.73.7283.01|IIS 4.0|  
|2.0 actualizado|2.73.7283.03|MDAC 1.5b y 1.5 c|  
|2.0 actualizado|2.73.7356|SDK DE ODBC 3.5|  
|2.5|2.573.2927|Visual Studio 6.0 y MDAC 2.0|  
|2.5 actualizado|2.573.3513|SQL Server 7.0<br /><br /> Service Pack 5 SQL Server 6.5|  
  
 Compilación 2.00.6235 (versión 1) fue la primera versión del controlador ODBC de Microsoft para Oracle. Después del lanzamiento de la primera versión, se ha adoptado una convención de nomenclatura de nuevo.  
  
 Por ejemplo, 2.73.7283.03 puede dividirse en los siguientes componentes distintos:  
  
-   2 = el número de versión.  
  
-   73 = la versión del servidor de Oracle para el que se diseñó el controlador.  
  
-   7283.03 = el número de compilación del controlador.  
  
> [!NOTE]  
>  Con la versión 2.573.2973, la convención de nomenclatura ha dado lugar a confusión que 2.573 es una versión anterior a la de 2,73, pero cada sección del número de compilación debe tenerse en cuenta individualmente. El número 573 es mayor que 73, por lo que es una versión más reciente. Además, "2.5" indica el número de versión del controlador.
