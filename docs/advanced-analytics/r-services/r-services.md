---
title: "R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/20/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# R Services
  Microsoft R Services proporciona dos plataformas de servidor para integrar el popular lenguaje de código abierto R con aplicaciones empresariales: **SQL Server R Services (en bases de datos)**, para la integración con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y **Microsoft R Server**.  
  
-   **R Services (en bases de datos)**  
  
     El objetivo de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] es permitir un rápido desarrollo, implementación y operatividad de las soluciones de R según la plataforma de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los servicios relacionados.  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] lleva el proceso a los datos al permitir que R se ejecute en el mismo equipo que la base de datos. Incluye un servicio de base de datos que se ejecuta aparte del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y que se comunica de forma segura con el tiempo de ejecución de R. Puede entrenar modelos de R, generar gráficos de R, realizar puntuaciones y mover datos fácilmente entre R y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los científicos de datos que prueban y desarrollan soluciones se pueden comunicar con el servidor desde un equipo de desarrollo remoto para ejecutar código de R en el servidor e implementar soluciones terminadas en SQL Server mediante la incrustación de llamadas a R en los procedimientos almacenados.  
  
     En esta descarga se incluye una distribución del lenguaje de código abierto R, así como ScaleR, un conjunto de paquetes de R escalables y de alto rendimiento. También se incluyen proveedores para procurar una conectividad más fácil y rápida con todas las tecnologías de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Para obtener más información, vea [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md). Para obtener escenarios de ejemplo, consulte [Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md).  
  
-   **Microsoft R Server**  
  
     Este sistema de servidor independiente admite soluciones de R escalables y distribuidas en varias plataformas, así como el uso de varios orígenes de datos empresariales, como Linux, Hadoop y Teradata.  
  
     Para obtener más información, consulte [Microsoft R Server (MSDN)](https://msdn.microsoft.com/microsoft-r/index).  
  
## <a name="related-technologies"></a>Tecnologías relacionadas  
 Microsoft proporciona una amplia compatibilidad con el ecosistema de lenguaje R de código abierto, incluidas herramientas, proveedores, paquetes de R mejorados y entornos de desarrollo integrados.  
  
-   **Herramientas de R para Visual Studio**  
  
     Visual Studio proporciona un entorno de desarrollo completo para el lenguaje R. El complemento incluye, entre otras muchas cosas, un editor, una ventana interactiva, un área de trazado y un depurador. Puede usar los lenguajes .NET de R o invocar R desde .NET a través de bibliotecas de código abierto como R.NET y rClr.  
  
     Para obtener más información, consulte [R Tools para Visual Studio](https://www.visualstudio.com/vs/rtvs/).  
  
-   **R en Azure Machine Learning**  
  
     Cree su propia área de trabajo en Estudio de aprendizaje automático de Azure, donde podrá tener acceso a más de 400 paquetes de R cargados previamente. Cree modelos y pruebe a implementarlos como un servicio web, o bien escriba scripts personalizados para transformar los datos. Cree sus propios paquetes de R y cárguelos en Azure para ejecutarlos como módulos personalizados. Publique sus soluciones en [Marketplace de Aprendizaje automático](http://datamarket.azure.com/browse/data?category=machine-learning).  
  
     Para obtener más información, consulte [Extender el experimento con R](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r) y [Creación de módulos R personalizados en Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules).  
  
-   **Máquinas virtuales de ciencia de datos**  
  
     Puede implementar una versión preinstalada y preconfigurada de [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] en Microsoft Azure, lo que facilita el inicio inmediato del trabajo de exploración de datos y modelado en la nube sin necesidad de preparar un sistema completamente configurado en local.  
  
     Azure Marketplace contiene varias máquinas virtuales que admiten la ciencia de datos:
     + **Microsoft Data Science Virtual Machine** está configurada con Microsoft R Server, así como Python (distribución de Anaconda), un servidor de Jupyter Notebook, Visual Studio Community Edition, Power BI Desktop, Azure SDK y SQL Server Express Edition. 
     + **Microsoft R Server 2016 para Linux** contiene la versión más reciente de R Server (versión 9.0.1). Hay máquinas virtuales independientes disponibles para CentOS versión 7.2 y Ubuntu versión 16.04. 
     + La máquina virtual **R Server Only SQL Server 2016 Enterprise** incluye un instalador independiente para R Server 9.0.1 que admite el nuevo modelo de licencia del ciclo de vida de software moderno.
 

## <a name="see-also"></a>Vea también  
[Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md) 

[Introducción a Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  

 [Instalar el motor de base de datos de SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)  
  
  