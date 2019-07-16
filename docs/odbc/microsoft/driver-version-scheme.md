---
title: Esquema de la versión de controlador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8a155f5d76e8a250c64d3d59e160fbb5863414f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071855"
---
# <a name="driver-version-scheme"></a>Esquema de la versión de controlador
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 En la tabla siguiente se enumera todas las versiones publicadas de Microsoft ODBC Driver for Oracle.  
  
|Versión del controlador|Número de compilación|Historial de disponibilidad|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 y Visual Basic 5.0, Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 y 1,5 a MDAC|  
|2.0 actualizado|2.73.7283.01|IIS 4.0|  
|2.0 actualizado|2.73.7283.03|MDAC 1.5b y 1.5 c|  
|2.0 actualizado|2.73.7356|SDK DE ODBC 3.5|  
|2.5|2.573.2927|Visual Studio 6.0 y MDAC 2.0|  
|2.5 actualizado|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 Compilación 2.00.6235 (versión 1) fue la primera versión del controlador ODBC de Microsoft para Oracle. Después del lanzamiento de la primera versión, se adoptó una nueva convención de nomenclatura.  
  
 Por ejemplo, 2.73.7283.03 puede dividirse en los siguientes componentes distintos:  
  
-   2 = el número de versión.  
  
-   73 = la versión del servidor de Oracle para el que se diseñó el controlador.  
  
-   7283.03 = el número de compilación del controlador.  
  
> [!NOTE]  
>  Con la versión 2.573.2973, la convención de nomenclatura ha llevado a cierta confusión que 2.573 es una versión anterior a 2,73, pero se debe considerar individualmente cada sección del número de compilación. El número 573 es mayor que 73, por lo que es una versión más reciente. Además, "2.5" indica el número de versión del controlador.
