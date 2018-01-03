---
title: "Herramientas de R incluidas con el programa de instalación de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9090313eed0997ea03329338c358825932dd8379
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="r-tools-included-with-sql-server-setup"></a>Herramientas de R incluidas con el programa de instalación de SQL Server

Cuando se instala R con SQL Server, obtendrá las mismas herramientas de R que se instalan con cualquier **base** instalación de R, como RGui, Rterm y así sucesivamente. Por lo tanto, técnicamente, tiene todas las herramientas que necesarias para desarrollar y probar código R.

Este tema enumeran las herramientas incluidas con la instalación.

> [!TIP]
> 
> Normalmente es más fácil de depurar y probar el código de R mediante el uso de un entorno de desarrollo dedicado. Le resultará más fácil ejecutar el código de R en SQL Server si se probarlas con antelación en una herramienta externa, por lo que puede leer los mensajes de error detallado y depurar la solución.
> 
> Consulte este artículo para obtener una lista de herramientas gratuitas que puede usar para desarrollar soluciones en R y cómo configurarlas para que funcione con SQL Server: [configurar un cliente de ciencia de datos](set-up-a-data-science-client.md)

**Se aplica a:** R Services (en bases de datos) de SQL Server 2016 y Microsoft R Server (independiente); SQL Server de 2017 (en bases de datos) de servicios de aprendizaje automático y Server (independiente) de aprendizaje automático

## <a name="r-tools-included-with-installation"></a>Herramientas de R incluidas con la instalación

Se incluyen las siguientes herramientas estándares de R en un *base instalación* de R y por lo tanto, se instalan de forma predeterminada.

+ **RTerm**: un terminal de línea de comandos para ejecutar scripts de R

+ **RGui.exe**: sencillo editor interactivo de R. Los argumentos de la línea de comandos son los mismos en RGui.exe y en RTerm.

+ **RScript**: herramienta de línea de comandos para ejecutar scripts de R en el modo por lotes.

Para encontrar estas herramientas, determine la biblioteca de R que se instala al configurar SQL Server o la característica de aprendizaje de automático de independiente. Por ejemplo, en una instalación predeterminada, las herramientas de R se encuentran en estas carpetas:

+ SQL Server 2016 R Services:`~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server independiente:`~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ Equipo con SQL Server de 2017 servicios de aprendizaje:`~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ Server (independiente) de aprendizaje automático:`~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

Si necesita ayuda con las herramientas de R, simplemente abra **RGui**, haga clic en **ayuda**y seleccione una de las opciones.

## <a name="introducing-microsoft-r-client"></a>Introducción a Microsoft R cliente

Cliente de Microsoft R es una descarga gratuita que proporciona acceso a los paquetes de RevoScaleR para fines de desarrollo. Al instalar el cliente de R, puede crear soluciones de R que se pueden ejecutar en todos los contextos de proceso admitidos, incluidos el análisis de en bases de datos de SQL Server y computación distribuida R en Hadoop, Spark o Linux con el servidor de aprendizaje de máquina.

Si ya ha instalado un entorno de desarrollo de R diferente, como RStudio, asegúrese de volver a configurar el entorno para usar las bibliotecas y ejecutables proporcionados por Microsoft R cliente. Por lo que puede usar todas las características del paquete RevoScaleR, aunque el rendimiento será limitada.

Para obtener más información, vea [¿qué es Microsoft R cliente?](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)
