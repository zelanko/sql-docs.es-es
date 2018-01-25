---
title: "Solución de problemas y preguntas más frecuentes para el aprendizaje automático en SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 06/16/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 640dde0a2faf43c7c5cda39789eaba759959bb99
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="troubleshoot-machine-learning"></a>Solucionar problemas de aprendizaje automático

Este artículo proporciona información para solucionar problemas relacionados con el programa de instalación y configuración de características de aprendizaje de máquina de SQL Server. La información incluye vínculos a guías de instalación, problemas conocidos y notas de la versión. Otros artículos vinculados a partir de este artículo le proporcionará consejos sobre la optimización de rendimiento de las soluciones de aprendizaje de máquina de SQL Server.

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

+ [Configurar servicios de aprendizaje de máquina con R o R Services](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)
+ [Configurar los servicios de aprendizaje de máquina a Python](../advanced-analytics/python/setup-python-machine-learning-services.md)
+ [Preguntas más frecuentes sobre el programa de instalación](../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Usar SqlBindR para actualizar una instancia de R services](../advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

Los artículos siguientes describen los pasos adicionales necesarios para la instalación sin conexión de características de aprendizaje de máquina de SQL Server:

+ [Instalación desatendida de R Services](../advanced-analytics/r/unattended-installs-of-sql-server-r-services.md) 
+ [Instalación desatendida de servicios de aprendizaje de máquina a Python](../advanced-analytics/python/unattended-installs-of-sql-server-python-services.md)

Si tiene que instalar el características en un equipo sin conexión de Internet de aprendizaje automático, use los vínculos de este artículo para descargar los componentes de R y Python antes de comenzar el programa de instalación:

+ [Instalación de componentes de aprendizaje automático sin acceso a Internet](../advanced-analytics/r/installing-ml-components-without-internet-access.md)

### <a name="configuration"></a>Configuración

Los artículos siguientes contienen información acerca de los valores predeterminados y cómo personalizar la configuración para una instancia de aprendizaje automático:

+ [Modificar el grupo de cuentas de usuario de SQL Server R Services](../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [Configurar y administrar extensiones de análisis avanzado](../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Cómo crear un grupo de recursos](r/how-to-create-a-resource-pool-for-r.md)
+ [Optimización de las cargas de trabajo de R](r/operationalizing-your-r-code.md)

## <a name="related-tools-and-services"></a>Servicios y herramientas relacionadas

+ [Configurar Microsoft máquina aprendizaje servidor independiente](../advanced-analytics/r/create-a-standalone-r-server.md)
+ [Configurar el servidor de R en una máquina virtual de Azure](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
+ [Instalar a R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)
+ [Obtener herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/)
