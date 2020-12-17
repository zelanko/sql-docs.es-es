---
title: Solución de problemas de aprendizaje automático en SQL Server
description: Proporciona un punto de partida para trabajar con problemas de aprendizaje automático en SQL.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/31/2018
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: e2d4d278f48cd453afb0666d0c9752c86b4a7e65
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470626"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Solución de problemas de aprendizaje automático en SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Use este artículo como punto de partida para solucionar los problemas que se encuentre al usar el aprendizaje automático de SQL Server.

## <a name="known-issues"></a>Problemas conocidos

En los artículos siguientes se describen los problemas conocidos de las versiones actuales y anteriores:

+ [Problemas conocidos de R Services](known-issues-for-sql-server-machine-learning-services.md)
+ [Notas de la versión de SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md)
+ [Notas de la versión de SQL Server 2017](../../sql-server/sql-server-2017-release-notes.md)
+ [Notas de la versión de SQL Server 2019](../../sql-server/sql-server-version-15-release-notes.md)

## <a name="how-to-gather-system-information"></a>Cómo recopilar información del sistema

Si se ha producido un error o necesita comprender un problema de su entorno, es importante que recopile sistemáticamente la información relacionada. En este artículo se proporciona una lista con información para solucionar problemas fácilmente sin ayuda, o para crear una solicitud de soporte técnico.

+ [Recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guías de instalación y configuración

Empiece aquí si no ha configurado el aprendizaje automático con SQL Server o si quiere agregar la característica:

+ [Instalación de SQL Server Machine Learning Services (en base de datos)](../install/sql-machine-learning-services-windows-install.md)
+ [Instalación de SQL Server Machine Learning Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md)
+ [Configuración del símbolo del sistema](../install/sql-ml-component-commandline-install.md)
+ [Instalación sin conexión (sin Internet)](../install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuración

Aquí encontrará artículos con información sobre los valores predeterminados y cómo personalizar la configuración de aprendizaje automático en una instancia de SQL:

+ [Escalar la ejecución simultánea de scripts externos en SQL Server Machine Learning Services](../administration/scale-concurrent-execution-external-scripts.md)   
+ [Procedimiento para crear un grupo de recursos](../administration/create-external-resource-pool.md)
+ [Optimización para cargas de trabajo de R](../r/operationalizing-your-r-code.md)
