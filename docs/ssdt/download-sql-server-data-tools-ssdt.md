---
title: Descargar SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "instalar ssdt, descargar ssdt, ssdt más reciente"
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 5bd0e1d3955d898824d285d28979089e2de6f322
ms.openlocfilehash: 7aaa4c48419bf24357b2bef95c40d721d1ab2f2a
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>Descargar SQL Server Data Tools (SSDT)

**[SQL Server Data Tools](https://msdn.microsoft.com/mt186501)** es una herramienta de desarrollo moderna que puede descargar de forma gratuita para crear bases de datos relacionales de SQL Server, bases de datos SQL de Azure, paquetes de Integration Services, modelos de datos de Analysis Services e informes de Reporting Services. Gracias a SSDT, puede diseñar e implementar cualquier tipo de contenido de SQL Server con la misma facilidad con la que desarrollaría una aplicación en Visual Studio. Esta versión es compatible con las versiones comprendidas entre SQL Server 2005 y SQL Server 2017, y ofrece el entorno de diseño necesario para agregar características nuevas de SQL Server 2016.  
    
    
![descarga](../ssdt/media/download.png) [Descargar SQL Server Data Tools 17.1 para Visual Studio 2015](https://go.microsoft.com/fwlink/?linkid=849393)

![descarga](../ssdt/media/download.png) [Descargar Data-Tier Application Framework (DacFx) 17.1](https://www.microsoft.com/download/details.aspx?id=55255)

## <a name="sql-server-data-tools"></a>SQL Server Data Tools   
**Información de versión**  
  
Número de versión: 17.1  
Número de compilación para esta versión: 14.0.61705.170
  
 **Novedades**
 - Compatibilidad sin conexión con IntelliSense de AS no relacionado con el modelo (por ejemplo, resaltado, finalización de instrucciones e información de parámetros)
 - Adición al Explorador de modelos tabulares para mostrar expresiones M
 - Selector de personas de Azure Active Directory para configurar miembros de rol en modelos tabulares
 - Compatibilidad con la codificación de sugerencias en la interfaz de usuario al definir modelos 1400
 - Varias correcciones de errores de proyectos de AS
 - Varias correcciones de errores de DacFx

 **Problemas conocidos**
 - Al crear un origen de datos en un modelo de AS del nivel de compatibilidad 1400, si selecciona un origen de datos basado en archivos y presiona Cancelar antes de crear el origen de datos, el editor tabular (Model.bim) pasará a ser de solo lectura. Para solucionar este problema, simplemente cierre el editor tabular y ábralo desde el Explorador de soluciones.

Lista completa de cambios disponible en el [registro de cambios](changelog-for-sql-server-data-tools-ssdt.md)

 > Para usar SQL Server Data Tools en Visual Studio 2017, vea [esta sección](#use-ssdt-in-visual-studio-2017) más adelante.

  **Idiomas disponibles**  
  
 Esta versión de SSDT puede instalarse en los idiomas siguientes:  
[Chino (República Popular China)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x804) | 
[Chino (Taiwán)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x404) | 
[Inglés (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x409) | 
[Francés]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x40c)  
[Alemán]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x410) | 
[Japonés]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x412) | 
[Portugués (Brasil)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x416) | 
[Ruso]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x419) | 
[Español]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x40a)  

**Imágenes ISO**

Una imagen ISO de SSDT puede usarse como forma alternativa de instalar SSDT o configurar un punto de instalación administrativa. ISO es un archivo autocontenido que contiene todos los componentes que necesita SSDT y puede descargarse con un administrador de descargas reiniciable, útil en situaciones con ancho de banda de red limitado o menos confiable. Una vez descargado, el ISO puede montarse como una unidad o copiarse en un DVD.

[Chino (República Popular China)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x804) |
[Chino (Taiwán)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x404) |
[Inglés (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x409) |
[Francés]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x40c)  
[Alemán]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x407) |
[Italiano]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x410) |
[Japonés]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x411) |
[Coreano]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x412) |
[Portugués (Brasil)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x416) |
[Ruso]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x419) |
[Español]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x40a)

## <a name="download-visual-studio"></a>Descargar Visual Studio

* [**Descargar Visual Studio Community 2015**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>Instalación de SSDT sin Visual Studio instalado previamente

Si no tiene Visual Studio instalado en la máquina, al instalar SSDT para Visual Studio 2015 también se instalará una versión mínima de "shell integrado" de Visual Studio 2015. La instalación de esta versión de Visual Studio es gratuita y se puede usar en tantas máquinas como quiera. Proporciona todos los tipos de proyecto de SQL Server, además del Explorador de objetos de SQL Server y otras experiencias de herramientas de SQL.

Si tiene [Visual Studio 2015 Community Edition (o superior)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) instalado en su máquina, al instalar SSDT se agregará el conjunto completo de herramientas de SQL Server en la instalación de Visual Studio existente. Visual Studio incluye numerosas características que podrían interesarle, como la integración del control de código fuente y la compatibilidad con lenguajes que no son SQL. Se recomienda usar Visual Studio 2015 Community o posterior para obtener la mejor experiencia de desarrollo de T-SQL.

## <a name="supported-sql-versions"></a>Versiones de SQL admitidas
  
|Plantillas de proyectos|Plataformas SQL compatibles|  
|-------------------|--------------------|  
Bases de datos relacionales|  SQL Server 2005* - SQL Server 2017 <br /><br />Base de datos SQL de Azure<br /><br />Azure SQL Data Warehouse (solo admite consultas, todavía no se admiten proyectos de base de datos)<br /><br />  * La compatibilidad con SQL Server 2005 está en desuso,<br /><br /> Cambie a una versión de SQL oficialmente compatible.|
  |Modelos de Analysis Services<br /><br />Informes de Reporting Services | SQL Server 2008 - SQL Server 2017|
  |paquetes de Integration Services| SQL Server 2012 - SQL Server 2017    |
  
## <a name="next-steps"></a>Pasos siguientes  
Después de instalar SSDT, siga estos tutoriales para aprender a crear bases de datos, paquetes, modelos de datos e informes mediante SSDT:  
  
-   [Desarrollo de bases de datos sin conexión orientado a proyectos](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [Tutorial de SSIS: Crear un paquete ETL sencillo](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Tutoriales de Analysis Services (SSAS)](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [Crear un informe de tabla básico (Tutorial de SSRS)](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="use-ssdt-in-visual-studio-2017"></a>Usar SSDT en Visual Studio 2017 

* [**Descargar Visual Studio 2017**](https://www.visualstudio.com/) ([comparar las características de Visual Studio 2017 por edición](https://www.visualstudio.com/vs/compare/))

Para usar los proyectos de bases de datos relacionales, se recomienda comprobar la carga de trabajo de **procesamiento y almacenamiento de datos** durante la instalación. También se incluye la compatibilidad con proyectos de bases de datos de SSDT en varias otras cargas de trabajo, las que incluyen *Azure*, *ASP.Net y Desarrollo web* y *Desarrollo multiplataforma de .NET Core*.

> [!NOTE]
> Los proyectos de base de datos de SSDT en Visual Studio 2017 actualmente admiten hasta SQL Server 2016.  Próximamente se incluirá compatibilidad con SQL Server 2017 en una actualización de Visual Studio 2017.

Si usa SSDT con Visual Studio 2017, instale los componentes de AS y RS:
* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="see-also"></a>Vea también  
[Herramientas de datos de SQL Server](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[Foro MSDN de SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog del equipo de SSDT](http://blogs.msdn.com/b/ssdt/)  
[Comentarios Connect sobre SSDT](https://connect.microsoft.com/SQLServer/Feedback)  
[Documentación de SSDT](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[Referencia de la API de DACFx](https://msdn.microsoft.com/library/dn645454.aspx)  
[Descarga de SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  

