---
title: Información general de la arquitectura (SQL Server R Services) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: e0441fc1ca1b61bc34ee51153e65b86e7622cee8
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="architecture-overview-for-r-in-sql-server"></a>Introducción a la arquitectura de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta sección proporciona información general sobre la arquitectura de servicios de SQL Server 2016 R y de servicios de aprendizaje de máquina de SQL Server de 2017.

La arquitectura de la arquitectura de extensibilidad es la misma o muy similar para SQL Server 2016 y versiones SQL Server de 2017 y similares también para R y Python. Sin embargo, para simplificar el análisis, este artículo describe sólo los componentes de R, incluidos los nuevos componentes agregados en el motor de base de datos de SQL Server para admitir la ejecución de scripts externos, la seguridad, las bibliotecas de R y la interoperabilidad con código abierto R.

Se proporcionan detalles adicionales en los vínculos de cada sección.

## <a name="r-interoperability"></a>Interoperabilidad de R

SQL Server 2016 R Services y SQL Server de 2017 Machine Learning Services (In-Database) instalan una distribución de código abierto de R, así como paquetes proporcionados por Microsoft que admiten el procesamiento distribuido o paralelo.

La arquitectura está diseñada para que ejecuten scripts externos con R en un proceso independiente de SQL Server. Los usuarios actuales de R deben ser capaces de transferir su código de R y ejecutarlo en T-SQL con modificaciones relativamente pequeñas.

Para escalar la solución o usar el procesamiento paralelo, se recomienda que realice la [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) paquete o [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package) paquete. Si no utiliza las capacidades de computación distribuidas proporcionadas por estas bibliotecas, todavía puede obtener algunas mejoras de rendimiento cuando se ejecuta el código de R en el contexto de SQL Server.

Para obtener más información acerca de los componentes de secuencias de comandos externos que están instalados, o la interacción de SQL Server con R, consulte [interoperabilidad de R](../../advanced-analytics/r/r-interoperability-in-sql-server.md)

## <a name="components-to-support-r-integration"></a>Componentes para la integración de R

El marco de extensibilidad que se introdujo en SQL Server 2016 continúa en SQL Server 2017. SQL Server usan los componentes de extensibilidad para iniciar el runtime de R, que se va a pasar datos entre R y el motor de base de datos como coordinar tareas paralelas necesarias para un trabajo de R externo.

Es la función de estos componentes adicionales mejorar la velocidad de intercambio de datos y compresión, al tiempo que proporciona una plataforma segura y de alto rendimiento para ejecutar scripts externos.

Para una descripción detallada de los componentes que admiten R, como el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] y RLauncher, consulte [nuevos componentes](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md).

## <a name="security"></a>Seguridad

Al ejecutar código de R mediante servicios de aprendizaje de máquina o SQL Server R Services, todos los scripts de R se ejecutan fuera del proceso de SQL Server, para proporcionar seguridad y una mayor capacidad de administración. Este aislamiento de procesos es aplicable independientemente de si ejecuta el script de R como parte de un procedimiento almacenado, o conectar con el trabajo de equipo de SQL Server desde un equipo remoto e iniciar un trabajo que utiliza el servidor como el contexto de proceso.

SQL Server intercepta todas las solicitudes de trabajo, se protege la tarea y sus datos mediante objetos de trabajo de Windows y se mantiene la seguridad a través de los datos mediante roles de base de datos y cuentas de usuario de SQL Server.

Datos se mantienen dentro del límite de cumplimiento de normas mediante la aplicación de seguridad de SQL Server en el nivel de instancia, la base de datos y la tabla. El Administrador de base de datos puede controlar quién tiene la capacidad de ejecutar trabajos de R y quién tiene la capacidad de instalar o compartir paquetes de R. El administrador también puede supervisar el uso de scripts de R en los usuarios remotos o locales y supervisar y administrar los recursos consumidos.

## <a name="next-steps"></a>Pasos siguientes

[Componentes que admiten la integración de R](new-components-in-sql-server-to-support-r.md)

[Interoperabilidad de R](r-interoperability-in-sql-server.md)

[Información general sobre seguridad](security-overview-sql-server-r.md)
