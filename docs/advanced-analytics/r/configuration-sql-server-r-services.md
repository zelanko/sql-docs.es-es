---
title: Configurar y administrar instancias de servicio de aprendizaje de máquina de SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b24832c8debe12c11aaa337e9558d99e7fae5ae0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585507"
---
# <a name="configure-and-manage-machine-learning-components-in-sql-server"></a>Configurar y administrar componentes de aprendizaje de máquina de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo contiene vínculos a información más detallada sobre cómo configurar un servidor para que admita servicios de aprendizaje de máquina con SQL Server en estos productos:

+ SQL Server 2016 R Services (In-Database)
+ Servicios de aprendizaje de máquina (en bases de datos) de SQL Server de 2017

> [!NOTE]
> 
> Este contenido se escribió originalmente para la versión de 2016 de SQL Server, que admite solo el lenguaje R.
> 
> En SQL Server 2017, compatibilidad con Python se ha agregado, pero el marco de trabajo de servicios y la arquitectura subyacente es el mismo. Por lo tanto, puede configurar la seguridad, memoria, el regulador de recursos y otras opciones para admitir la ejecución de scripts de Python, del mismo modo que lo haría para scripts de R.
> 
> Sin embargo, dado que la compatibilidad con Python es una característica nueva, la información detallada sobre las posibles optimizaciones para la carga de trabajo de Python todavía no está disponible. Vuelva a comprobarlo más tarde.

## <a name="r-package-management"></a>Administración de paquetes de R

Estos artículos describe cómo instalar nuevos paquetes de R en la instancia de SQL Server, administrar las bibliotecas de paquete de R y restaurar las bibliotecas de paquete después de una restauración de base de datos.

+ [Paquetes de R de manera predeterminada y Python en SQL Server](installing-and-managing-r-packages.md)
+ [Instalar nuevos paquetes de R](install-additional-r-packages-on-sql-server.md)
+ [Habilitar la administración de paquete para una instancia con Roles de base de datos](r-package-how-to-enable-or-disable.md)
+ [Crear un repositorio de paquete Local mediante miniCRAN](create-a-local-package-repository-using-minicran.md)
+ [Determinar que los paquetes de R instalados en SQl Server](determine-which-packages-are-installed-on-sql-server.md)
+ [Sincronizar los paquetes de R entre SQL Server y el sistema de archivos](package-install-uninstall-and-sync.md)
+ [Paquetes de R instalados en bibliotecas de usuario](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>Configuración del servicio

Estos artículos describen cómo realizar cambios en la arquitectura subyacente del servicio y cómo administrar a las entidades de seguridad asociadas con el servicio de extensibilidad.

+ [Consideraciones de seguridad](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Modificar el grupo de cuentas de usuario de SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [Configuración y administración de Extensiones de análisis avanzados](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [Habilitar la administración de paquete para una instancia con Roles de base de datos](r-package-how-to-enable-or-disable.md)
+ [Optimizar el rendimiento de R Services](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>Regulación de recursos

Estos artículos describen cómo implementar la administración de recursos para los trabajos de R o Python mediante la característica de regulador de recursos que estará disponible en la edición Enterprise.

+ [Regulación de recursos para R Services](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [Cómo crear un grupo de recursos para R](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

Vea también:

+ [Uso de informes SSMS personalizado de R de Monitor](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>Instalación inicial

Encontrará ayuda adicional relacionada con la instalación y configuración iniciales en estos artículos:

+ [Preguntas más frecuentes sobre actualización e instalación](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Consideraciones de seguridad](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Problemas conocidos de R Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

