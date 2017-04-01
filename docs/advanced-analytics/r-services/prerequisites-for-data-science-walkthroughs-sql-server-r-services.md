---
title: "Requisitos previos para los tutoriales de ciencia de datos (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Requisitos previos para los tutoriales de ciencia de datos (SQL Server R Services)
Recomendamos que realice los tutoriales en una estación de trabajo de R que se pueda conectar a un equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la misma red. También puede ejecutar el tutorial en un equipo que tenga [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un entorno de desarrollo de R. 
  
  
## <a name="install-sql-server-2016-r-services-in-database"></a>Instalar SQL Server 2016 R Services (en bases de datos)  
Debe tener acceso a una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] instalado. Para obtener más información sobre cómo configurar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], consulte [Configurar SQL Server R Services (en bases de datos)](https://msdn.microsoft.com/library/mt696069.aspx).  
  
  
> [!IMPORTANT]  
> Asegúrese de usar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o una versión posterior. Las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admiten la integración con R. Sin embargo, puede usar bases de datos SQL antiguas como origen de datos ODBC.  
  
## <a name="install-an-r-development-environment"></a>Instalar un entorno de desarrollo de R  
Para completar este tutorial en el equipo, necesitará un entorno de desarrollo de R o cualquier herramienta de línea de comandos que pueda ejecutar comandos de R.    
  
- **Herramientas de R para Visual Studio** es un complemento gratuito que proporciona Intellisense, depuración y compatibilidad con Microsoft R Server y SQL Server R Services. Para descargarlo, consulte la página sobre [Herramientas de R para Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx).  
    
- **Cliente de Microsoft R** es una herramienta de desarrollo ligera que admite el desarrollo en R mediante el uso de los paquetes ScaleR. Para obtenerla, consulte [Get Started with Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started) (Introducción a Cliente de Microsoft R).
  
- **RStudio** es uno de los entornos de desarrollo de R más populares. Para obtener más información, consulte [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).  
  
    Sin embargo, no puede completar este tutorial con una instalación genérica de RStudio u otro entorno; debe instalar también los paquetes de R y las bibliotecas de conectividad de Microsoft R Open. Para obtener más información, consulte [Configurar un cliente de ciencia de datos](https://msdn.microsoft.com/library/mt696067.aspx).  

- Las herramientas de R (R.exe, RTerm.exe, RScripts.exe) se instalan de forma predeterminada al instalar [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]. Si no quiere instalar un IDE, puede usar estas herramientas.  
  
  
## <a name="get-permissions-to-connect-to-sql-server"></a>Obtener permisos para conectar con SQL Server  
En este tutorial, se conectará con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar scripts y cargar datos. Para ello, debe tener un inicio de sesión válido en el servidor de bases de datos.  Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Pídale al administrador de base de datos que cree una cuenta para usted en el servidor con los siguientes privilegios en la base de datos en la que usará R:  
  
-   Crear bases de datos, tablas, funciones y procedimientos almacenados    
-   Insertar datos en tablas  
  
  
## <a name="start-the-walkthrough"></a>Iniciar el tutorial  
[Lección 1: Preparar los datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
