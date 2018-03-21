---
title: "Solución de problemas y preguntas más frecuentes para el aprendizaje automático en SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 5b9a5c6497781ef67d9d2ef9b9032a4d9ee250e5
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2018
---
# <a name="troubleshoot-machine-learning"></a>Solucionar problemas de aprendizaje automático
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo contiene vínculos para solucionar problemas en las guías de instalación, problemas conocidos y notas de la versión. Otros artículos vinculados a partir de este artículo le proporcionará consejos sobre la optimización de rendimiento de las soluciones de aprendizaje de máquina de SQL Server.

Utilice esta página como punto de partida para buscar problemas conocidos, las preguntas más frecuentes el programa de instalación y los procedimientos para solucionar el problema.

**Se aplica a:** Services (R y Python) de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="known-issues"></a>Problemas conocidos

Los siguientes artículos de lista de problemas conocidos con la versión actual, o describen los problemas con las versiones anteriores:

+ [Problemas conocidos de R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Notas de la versión de SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="troubleshooting-prerequisites"></a>Solución de problemas de requisitos previos

Si se ha producido un error o se deben comprender un problema en su entorno, es importante que recopile información relacionada sistemáticamente. Esta información incluye la versión, la edición, el contexto de seguridad y el contexto de ejecución.

El siguiente artículo proporciona una lista de información que facilita la solución de problemas de autoayuda o una solicitud de soporte técnico.

+ [Recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guías de instalación y configuración

Empiece aquí si no ha configurado aprendizaje automático con SQL Server, o si desea agregar la característica:

+ [Instalar servicios de aprendizaje automático SQL Server de 2017 (en bases de datos)](install/sql-machine-learning-services-windows-install.md)
+ [Instalar a servidor de aprendizaje de SQL Server de 2017 máquina (independiente)](install/sql-machine-learning-standalone-windows-install.md)
+ [Instalar SQL Server 2016 R Services (en bases de datos)](install/sql-r-services-windows-install.md)
+ [Instalar a SQL Server 2016R Server (independiente)](install/sql-r-standalone-windows-install.md)
+ [Programa de instalación de línea de comandos](install/sql-ml-component-commandline-install.md)
+ [Programa de instalación sin conexión (no a internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuración

Los artículos siguientes contienen información acerca de los valores predeterminados y cómo personalizar la configuración para una instancia de aprendizaje automático:

+ [Modificar el grupo de cuentas de usuario de SQL Server R Services](r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [Configurar y administrar extensiones de análisis avanzado](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Cómo crear un grupo de recursos](r/how-to-create-a-resource-pool-for-r.md)
+ [Optimización de las cargas de trabajo de R](r/operationalizing-your-r-code.md)
