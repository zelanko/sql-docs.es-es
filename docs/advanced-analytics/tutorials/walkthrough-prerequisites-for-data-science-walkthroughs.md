---
title: Requisitos previos para el tutorial de ciencia de datos de SQL Server y R | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9d3a579f023a7e6d9805b934edc3f0e9e5ad5e8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>Requisitos previos para el tutorial de ciencia de datos de SQL Server y R

Se recomienda que realice este tutorial en un equipo portátil o en otro equipo que tenga instaladas las bibliotecas de Microsoft R. Debe ser capaz de conectarse, en la misma red, a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo con los servicios de aprendizaje de máquina y el lenguaje R habilitado.

Puede ejecutar el tutorial en un equipo que tenga tanto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un entorno de desarrollo de R pero no se recomienda esta configuración para un entorno de producción.

## <a name="install-machine-learning-for-sql-server"></a>Aprendizaje automático de instalación para SQL Server

Debe tener acceso a una instancia de SQL Server con compatibilidad con R instalado, mediante una de las acciones siguientes:

+ Servicios (en bases de datos) de aprendizaje automático para SQL Server de 2017
+ SQL Server 2016 R Services

Para obtener más información, consulte [configurar SQL Server R Services (In-Database](../r/set-up-sql-server-r-services-in-database.md).

> [!IMPORTANT]
> Asegúrese de usar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o una versión posterior. Las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admiten la integración con R. Sin embargo, puede usar bases de datos SQL antiguas como origen de datos ODBC.

## <a name="install-an-r-development-environment"></a>Instale un entorno de desarrollo de R

En este tutorial, se recomienda que use un entorno de desarrollo de R. Éstas son algunas sugerencias:

- **R Tools para Visual Studio** (RTV) es una segunda complemento que proporciona Intellisense, depuración y la compatibilidad con Microsoft R. también puede utilizarlo con R Server y servicios de aprendizaje de máquina de SQL Server. Para descargarlo, consulte la página sobre [Herramientas de R para Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx).

- **Cliente de Microsoft R** es una herramienta de desarrollo ligera que admite el desarrollo en R mediante el uso de los paquetes ScaleR. Para obtenerla, consulte [Get Started with Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)(Introducción a Cliente de Microsoft R).

- **RStudio** es uno de los entornos de desarrollo de R más populares. Para obtener más información, consulte [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).

    No se puede completar este tutorial utiliza una instalación genérica de RStudio o en otro entorno; También debe instalar los paquetes de R y las bibliotecas de conectividad de Microsoft R Open. Para obtener más información, consulte [Configurar un cliente de ciencia de datos](../r/set-up-a-data-science-client.md).

- Herramientas básicas de R (R.exe, RTerm.exe, RScripts.exe) también se instalan de forma predeterminada al instalar [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]. Si no desea instalar un IDE, puede usar estas herramientas.

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>Obtener permisos en la instancia de SQL Server y la base de datos

Para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar scripts y cargar datos, debe tener un inicio de sesión válido en el servidor de base de datos.  Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Pida al administrador de base de datos para configurar los siguientes permisos para la cuenta, en la base de datos en los que usa R:

- Crear bases de datos, tablas, funciones y procedimientos almacenados
- Escribir datos en tablas
- Capacidad de ejecutar script de R (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

En este tutorial, hemos usado el inicio de sesión SQL **RTestUser**. Por lo general, se recomienda que utilice la autenticación integrada de Windows, pero usar el inicio de sesión SQL es más fácil para determinados fines de demostración.

## <a name="change-list"></a>Lista de cambios

+ En este ejemplo se desarrolló originalmente mediante SQL Server 2016 R Services. Sin embargo, se introdujeron cambios importantes en los componentes de R de Microsoft para 2016 SP1. En concreto, el _varsToDrop_ y _varsToKeep_ ya no se admiten parámetros para los orígenes de datos de SQL Server. Therefre, si descargó una versión del tutorial anterior a SP1, ya no funcionará con versiones posteriores del Service Pack 1.

+ La versión actual de la muestra se ha probado con una compilación de versión preliminar de SQL Server de 2017 Machine Learning Services (RC1 y RC2). En general, casi todos los pasos deben ejecutar sin modificaciones entre 2016 SP1 y de 2017.

## <a name="next-lesson"></a>Lección siguiente

[Preparar los datos de uso de PowerShell](/walkthrough-prepare-the-data.md)

