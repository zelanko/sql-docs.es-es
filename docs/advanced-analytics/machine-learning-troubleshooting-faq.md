---
title: 'Solución de problemas y preguntas más frecuentes sobre machine learning: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4a62dd0710a97a33f5a4703f194df2c6bcef2a54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650332"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Solución de problemas de aprendizaje automático en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Utilice esta página como punto de partida para repasar los problemas conocidos.

**Se aplica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (R y Python)

## <a name="known-issues"></a>Problemas conocidos

Los artículos siguientes describen los problemas conocidos con las versiones actuales y anteriores:

+ [Problemas conocidos de R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Notas de la versión de SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>Cómo recopilar información del sistema

Si se ha producido un error o necesita comprender un problema en su entorno, es importante que recopile información relacionada sistemáticamente. El siguiente artículo proporciona una lista de información que facilita la solución de problemas de autoayuda o una solicitud de soporte técnico.

+ [Recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guías de instalación y configuración

Comience aquí si no ha configurado aprendizaje automático con SQL Server, o si desea agregar la característica:

+ [Instalar SQL Server 2017 Machine Learning Services (en bases de datos)](install/sql-machine-learning-services-windows-install.md)
+ [Instalar a SQL Server 2017 Machine Learning Server (independiente)](install/sql-machine-learning-standalone-windows-install.md)
+ [Instalar SQL Server 2016 R Services (en bases de datos)](install/sql-r-services-windows-install.md)
+ [Instalar a SQL Server 2016 R Server (independiente)](install/sql-r-standalone-windows-install.md)
+ [Programa de instalación de línea de comandos](install/sql-ml-component-commandline-install.md)
+ [Instalación sin conexión (sin Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuración

Los artículos siguientes contienen información acerca de los valores predeterminados y cómo personalizar la configuración de una instancia de aprendizaje automático:

+ [Escala la ejecución simultánea de scripts externos en SQL Server Machine Learning Services](administration/modify-user-account-pool.md)   
+ [Configurar y administrar extensiones de análisis avanzado](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Cómo crear un grupo de recursos](r/how-to-create-a-resource-pool-for-r.md)
+ [Optimización de cargas de trabajo de R](r/operationalizing-your-r-code.md)
