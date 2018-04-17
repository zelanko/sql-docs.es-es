---
title: Introducción a la arquitectura de servicios de aprendizaje de máquina de SQL Server con Python | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9876e54ed0b45bda48f76c3b1d764b1312313348
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="architecture-overview-for-machine-learning-services-with-python"></a>Introducción a la arquitectura de servicios de aprendizaje de máquina a Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo proporciona información general sobre cómo Python se integra con SQL Server, incluido el modelo de seguridad, los componentes en el motor de base de datos que admiten la ejecución de scripts externos y nuevos componentes que permiten la interoperabilidad de Python con SQL Server. Para obtener más información, vea los artículos vinculados.

> [!IMPORTANT]
> Compatibilidad con Python está disponible a partir de 2017 CTP 2.0 de SQL Server. Esta característica de versión preliminar está sujeta a cambios.

## <a name="python-interoperability"></a>Interoperabilidad de Python

Servicios de aprendizaje de máquina (en bases de datos) de SQL Server instala la distribución de Anaconda de Python y el tiempo de ejecución de Python 3.5 y el intérprete. Esto asegura la compatibilidad completar junto con las soluciones estándar de Python. Python se ejecuta en un proceso independiente de SQL Server, para garantizar que las operaciones de base de datos no se vean comprometidas.

Para obtener más información acerca de la interacción de SQL Server con Python, consulte [interoperabilidad de Python](../../advanced-analytics/python/python-interoperability.md)

## <a name="components-that-support-python-integration"></a>Componentes que admiten la integración de Python

El marco de extensibilidad que se introdujo en SQL Server 2016 ahora admite la ejecución del script de Python, mediante la adición de nuevos componentes específicos del idioma. Estos componentes mejoran la velocidad de intercambio de datos y compresión, al tiempo que proporciona una plataforma segura y de alto rendimiento para ejecutar scripts externos.

Para una descripción detallada de los componentes que admiten Python, como el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] y PythonLauncher, consulte [nuevos componentes](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md).

## <a name="security"></a>Seguridad

Las tareas de Python que se ejecutan fuera del proceso de SQL Server, para proporcionar seguridad y una mayor capacidad de administración.

Todas las tareas están protegidas mediante objetos de trabajo de Windows o la seguridad de SQL Server. Datos se mantienen dentro del límite de cumplimiento de normas mediante la aplicación de seguridad de SQL Server en el nivel de instancia, la base de datos y la tabla. El Administrador de base de datos puede controlar quién tiene la capacidad de ejecutar trabajos de Python, supervisar el uso de scripts de Python por los usuarios y ver los recursos consumidos.

Para obtener más información, consulte [la seguridad de Python](../../advanced-analytics/python/security-overview-sql-server-python-services.md)

## <a name="resource-governance"></a>Regulador de recursos

En SQL Server Enterprise Edition, puede utilizar el regulador de recursos para administrar y supervisar el uso de recursos de operaciones de script externo, como un script de R y scripts de Python.

Para obtener más información, consulte [regulador de recursos para R](../../advanced-analytics/r/resource-governance-for-r-services.md).

## <a name="next-steps"></a>Pasos siguientes

[Ejecución de Python mediante T-SQL](../tutorials/run-python-using-t-sql.md)
