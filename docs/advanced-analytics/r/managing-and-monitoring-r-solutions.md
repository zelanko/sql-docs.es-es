---
title: "Administración y supervisión de soluciones de aprendizaje de máquina | Documentos de Microsoft"
ms.custom: SQL2016_New_Updated
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 42da1c7becbb7003ab66b7ce58cbdbb307326aaa
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="managing-and-monitoring-machine-learning-solutions"></a>Administración y supervisión de soluciones de aprendizaje de máquina

Este artículo describen características de SQL Server Machine Learning Services que están relacionados con los administradores de base de datos que necesitan para empezar a trabajar con soluciones de R y Python.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="security"></a>Seguridad

Los administradores de base de datos deben proporcionar acceso a datos no solo a los científicos de datos, sino a una variedad de desarrolladores de informes, los analistas de negocios y consumidores de datos empresariales. La integración de R (y ahora Python) en SQL Server ofrece numerosas ventajas para los administradores de base de datos que respalden las iniciativas de ciencias de datos.

+ La arquitectura de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege las bases de datos y aísla la ejecución de las sesiones de R del funcionamiento de la instancia de la base de datos.

+ Puede especificar quién tiene permiso para ejecutar los scripts de R y garantizar que los datos utilizados en las tareas de dicho lenguaje de programación se administran con los mismos roles de seguridad que los definidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

+ El Administrador de base de datos puede utilizar funciones para administrar la instalación de paquetes de R y la ejecución de scripts de R y Python.

Para obtener más información, vea estos recursos:

+ [Consideraciones de seguridad para el tiempo de ejecución de R en SQL Server](../../advanced-analytics/r/security-considerations-for-the-r-runtime-in-sql-server.md)

+ [Información general de seguridad de R](../r/security-overview-sql-server-r.md)

+ [Información general de seguridad de Python](../python/security-overview-sql-server-python-services.md)

+ [Instalar y administrar paquetes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)

## <a name="configuration-and-management"></a>Configuración y administración

Los administradores de bases de datos deben integrar prioridades y proyectos opuestos en un único punto de contacto: el servidor de la base de datos. Deben admitir análisis al tiempo que mantiene el estado de los almacenes de datos informes y operativos. La integración de con SQL Server de aprendizaje automático proporciona muchas ventajas para los administradores de base de datos, que actúa un papel fundamental en la implementación de una infraestructura eficaz de ciencia de datos de cada vez más.

+ Sesiones de R y Python se ejecutan en un proceso independiente para asegurarse de que el servidor sigue ejecutándose como de costumbre, incluso si el tiempo de ejecución de script externo tiene problemas.

+ Las cuentas de usuario físico con pocos privilegios se utilizan para contener y aislar la actividad de script externo.

+ El DBA puede utilizar herramientas de administración de recursos de SQL Server estándares para controlar la cantidad de recursos asignados al runtime de R, para evitar que unos cálculos masivos pongan en peligro el rendimiento general del servidor.

Para obtener más información, vea estos recursos:

+ [Regulador de recursos para R Services](../r/resource-governance-for-r-services.md)

+ [Supervisar R Services](../r/monitoring-r-services.md)

+ [Configurar y administrar extensiones de análisis avanzado](../r/configure-and-manage-advanced-analytics-extensions.md)
