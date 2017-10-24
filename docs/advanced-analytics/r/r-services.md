---
title: "Servicios de aprendizaje de máquina de Microsoft | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 23
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 246ea9f306c7d99b835c933c9feec695850a861b
ms.openlocfilehash: ddc9b3f17afe1f9d4c811e4a5871f48a3a08de7f
ms.contentlocale: es-es
ms.lasthandoff: 10/13/2017

---
# <a name="microsoft-machine-learning-services"></a>Servicios de aprendizaje automático de Microsoft

El objetivo de servicios de aprendizaje de máquinas de Microsoft es proporcionar una plataforma extensible y escalable para integrar las tareas de aprendizaje automático y herramientas con las aplicaciones que consumen servicios de aprendizaje de máquina. La plataforma debe atender las necesidades de todos los usuarios implicados en el proceso de análisis y el desarrollo de datos desde los científicos de datos, para arquitectos y administradores de base de datos.

Ventajas principales incluyen:

+ Análisis de escalable
+ Varias plataformas y contextos de proceso, para las soluciones de "escribir una vez, impleméntelo donde quiera"
+ Evita el movimiento de datos y el riesgo de datos si se ponen de análisis de los datos
+ Los científicos de datos pueden elegir sus propias herramientas y lenguajes
+ Se integra las mejores características de código abierto con las capacidades empresariales de Microsoft
+ Administración simplificada
+ Fácil de implementar y utilizar modelos de predicción

## <a name="in-database-analytics-with-sql-server"></a>Análisis de bases de datos con SQL Server

En SQL Server 2016, Microsoft lanzó dos plataformas para integrar el lenguaje de código abierto R en aplicaciones empresariales:

+ **SQL Server R Services (en bases de datos)**, para la integración con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ **Microsoft R Server**, para las implementaciones de R de nivel empresarial en servidores de Windows y Linux

En SQL Server 2017, se cambió el nombre para reflejar la compatibilidad con el popular lenguaje de Python.

+ **Servicios de aprendizaje de máquina (en bases de datos) de SQL Server** es compatible con R y Python para realizar análisis en bases de datos.
+ **Aprendizaje de máquina de Microsoft Server** es compatible con las implementaciones de R y Python en Windows Server, con la expansión de otras plataformas compatibles planeado para tiempo de ejecución de 2017.

### <a name="benefits"></a>Ventajas

Servicios de aprendizaje de máquinas de Microsoft pone el proceso a los datos al permitir que R para que se ejecute en el mismo equipo que la base de datos. Incluye el servicio Launchpad de confianza, que se ejecuta fuera de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesar y se comunica de forma segura con el tiempo de ejecución de R o Python.

Con servicios de aprendizaje de máquina de SQL Server, puede entrenar modelos, generar gráficos, realizar puntuaciones y mover fácilmente datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y R o Python.

Científicos de datos que comprueban y desarrollan soluciones pueden enviar secuencias de comandos desde un equipo de desarrollo remoto para ejecutar código de forma segura en el servidor, o pueden implementar soluciones terminadas en SQL Server mediante la inserción de código de aprendizaje de máquina en procedimientos almacenados de SQL.

Cuando se instala el aprendizaje automático para SQL Server, obtendrá una distribución de R de código abierto o lenguaje de Python, así como las bibliotecas de R y Python escalables suministradas por Microsoft. El motor de base de datos de SQL Server también incluye nuevos componentes diseñados para reforzar la conectividad y con mayor rapidez, garantizar una comunicación más segura con lenguajes externos como R o Python.

### <a name="where-to-get-it"></a>Dónde conseguirla

Para empezar, consulte estos recursos:

+ [SQL Server R Services](sql-server-r-services.md)
+ [Servicios de Python SQL Server](../python/sql-server-python-services.md)
+ [Tutoriales de aprendizaje automático](../tutorials/machine-learning-services-tutorials.md)

> [!NOTE]
> Compatibilidad con Python sólo se proporciona en SQL Server 2017. 

## <a name="machine-learning-server-standalone-and-microsoft-r-server-standalone"></a>Aprendizaje automático Server (independiente) y Microsoft R Server (independiente)

Este sistema de servidor independiente admite soluciones de R escalables y distribuidas en varias plataformas y el uso de varios orígenes de datos empresariales, como Linux y una visión general de HD. Si no es necesario para la integración con SQL Server, puede instalar R Server para habilitar el desarrollo rápido de implementación y puesta en marcha de soluciones de aprendizaje automático. También puede usar a los instaladores de R Server para actualizar los componentes de R asociados con una instancia de SQL Server y obtener la versión más reciente de R.

Si instala el servidor de aprendizaje de máquina de Microsoft mediante el programa de instalación de SQL Server 2017, también puede implementar y utilizar aplicaciones de Python.

Para obtener más información, consulte [aprendizaje de máquina de Microsoft Server](https://docs.microsoft.com/r-server/index).

## <a name="related-technologies"></a>Tecnologías relacionadas

Microsoft proporciona una amplia compatibilidad con para ecosistemas de aprendizaje de máquina, incluidas las herramientas, proveedores, paquetes mejorados de R y Python, un desarrollo de nube y plataforma de servicios y un entorno de desarrollo integrado.

### <a name="r-tools-for-visual-studio"></a>Herramientas de R para Visual Studio

Visual Studio proporciona un entorno de desarrollo completo para el lenguaje R. El complemento incluye, entre otras muchas cosas, un editor, una ventana interactiva, un área de trazado y un depurador. Puede usar los lenguajes .NET de R o invocar R desde .NET a través de bibliotecas de código abierto como R.NET y rClr.

Visual Studio también aporta un excelente entorno de desarrollo de Python. No hay ninguna manera más fácil trabajar con idiomas de aprendizaje de máquina mientras continúa teniendo acceso a las herramientas de desarrollo de base de datos SQL.

Para obtener más información, vea:

+ [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/)
+ [Python - Visual Studio](https://www.visualstudio.com/vs/python/)

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure

Al crear su propia área de trabajo en estudio de aprendizaje automático de Azure, tendrá acceso a más de 400 paquetes de R cargados previamente. También puede elegir al crear un experimento con R, para implementar R mediante una distribución de CRAN R estándar o Microsoft R Open. Incluso puede crear sus propios paquetes de R y cárguelos en Azure para ejecutarlos como módulos personalizados.

Para obtener más información, vea estos recursos:

+ [Extender el experimento con R](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r)
+ [Crear módulos personalizados de R en aprendizaje automático de Azure](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules)

Muchos de los algoritmos proporcionados en aprendizaje automático de Azure ahora se incluyen servicios de aprendizaje de máquina de Microsoft, como parte del paquete MicrosoftML. Para obtener más información, consulte [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).

Aprendizaje automático de Azure es otra plataforma cómoda para científicos de datos y los desarrolladores que necesiten crear, entrenar e implementar modelos con los servicios Web. Puede publicar soluciones a la [Marketplace de aprendizaje automático](http://datamarket.azure.com/browse/data?category=machine-learning).

### <a name="data-science-virtual-machines"></a>Máquinas virtuales de ciencia de datos

Puede implementar una versión preinstalada y preconfigurada de [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] en Microsoft Azure, lo que facilita el inicio inmediato del trabajo de exploración de datos y modelado en la nube sin necesidad de preparar un sistema completamente configurado en local.

Azure Marketplace contiene varias máquinas virtuales que admiten la ciencia de datos:

+ **Microsoft Data Science Virtual Machine** está configurada con Microsoft R Server, así como Python (distribución de Anaconda), un servidor de Jupyter Notebook, Visual Studio Community Edition, Power BI Desktop, Azure SDK y SQL Server Express Edition.

+ **Microsoft R Server 2016 para Linux** contiene la versión más reciente de R Server (versión 9.0.1). Máquinas virtuales independientes están disponibles para CentOS versión 7.2 y Ubuntu versión 16.04.

+ El **R Server solo SQL Server 2016 Enterprise** máquina virtual incluye un instalador independiente para R Server 9.0.1 que admite el nuevo modelo de licencias de ciclo de vida de Software modernas.

> [!TIP]
> El nuevo [VM de ciencia de datos para Windows Server 2016](http://aka.ms/dsvm/win2016) proporciona versiones GPU de marcos de trabajo de aprendizaje profundo populares como CNTK. Las herramientas instaladas previamente incluyen los controladores de GPU NVIDIA, CUDA Kit de herramientas 8.0 y la biblioteca de cuDNN NVIDIA para cargas de trabajo GPU. En unos minutos, puede tener un entorno completo para la creación de modelos de aprendizaje profundo que se pueden ejecutar en la CPU o CPU más GPU.

## <a name="next-steps"></a>Pasos siguientes

[Introducción a servicios de aprendizaje de máquina](getting-started-with-sql-server-r-services.md)

[Introducción a servidor de aprendizaje de máquina](getting-started-with-microsoft-r-server-standalone.md)

[Instalar el motor de base de datos de SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)

