---
title: Descargar SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 09/28/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
keywords:
- instalar ssdt, descargar ssdt, ssdt más reciente
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: f63416c3400f328f0602aa804dc66716067eeb7e
ms.sourcegitcommit: 3a8293b769b76c5e46efcb1b688bffe126d591b3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226307"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>Descargar e instalar SQL Server Data Tools (SSDT) para Visual Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
**SQL Server Data Tools** es una herramienta de desarrollo moderna para crear bases de datos relacionales de SQL Server, bases de datos SQL de Azure, modelos de datos de Analysis Services (AS), paquetes de Integration Services (IS) e informes de Reporting Services (RS). Gracias a SSDT, puede diseñar e implementar cualquier tipo de contenido de SQL Server con la misma facilidad con la que desarrollaría una aplicación en Visual Studio.

*Para la mayoría de los usuarios, SQL Server Data Tools (SSDT) se instala durante la instalación de Visual Studio. Al instalar SSDT mediante el instalador de Visual Studio, se agrega la funcionalidad básica de SSDT, por lo que necesitará ejecutar el [instalador independiente de SSDT](#ssdt-for-vs-2017-standalone-installer) para obtener las herramientas de AS, IS y RS.*

## <a name="install-ssdt-with-visual-studio-2017"></a>Instalar SSDT con Visual Studio 2017

Para instalar SSDT durante la [instalación de Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio), seleccione la carga de trabajo **Procesamiento y almacenamiento de datos** y, después, seleccione **SQL Server Data Tools**. Si Visual Studio ya está instalado, puede [modificar la lista de cargas de trabajo](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) para incluir SSDT: ![Carga de trabajo de procesamiento y almacenamiento de datos](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)



## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Instalar las herramientas de Analysis Services, Integration Services y Reporting Services
Para instalar la compatibilidad con proyectos de AS, IS y RS, ejecute el [instalador independiente de SSDT](#ssdt-for-vs-2017-standalone-installer). 

El instalador enumera las instancias disponibles de Visual Studio a las que se van a agregar las herramientas de SSDT. Si Visual Studio no está instalado, al seleccionar **Instalar una nueva instancia de SQL Server Data Tools** se instala SSDT con una versión mínima de Visual Studio, pero para una mejor experiencia se recomienda usar SSDT con [la versión más reciente de Visual Studio](https://www.visualstudio.com/downloads). 

![Selección de AS, IS, RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT para VS 2017 (instalador independiente)

[![descargar](../ssdt/media/download.png) Descargar SSDT para Visual Studio 2017 (15.8.1) ](https://go.microsoft.com/fwlink/?linkid=2024393) 

> [!IMPORTANT]
> - Antes de instalar SSDT para Visual Studio 2017 (15.8.1), desinstale las extensiones *Proyectos de Analysis Services* y *Proyectos de Reporting Services*, si están instaladas y cierre todas las instancias de VS.
> - Al instalar SSDT en Windows 10 1803 y elegir instalar SSIS, podría encontrarse con un reinicio inesperado. Puede iniciar de nuevo el programa de instalación y continuar con la instalación después del reinicio.



**Información de versión**  
  
Número de versión: 15.8.1  
Número de compilación: 14.0.16179.0  
Fecha de publicación: 27 de septiembre de 2018  

Para ver la lista completa de cambios, consulte el [registro de cambios](changelog-for-sql-server-data-tools-ssdt.md).

SSDT para Visual Studio 2017 tiene los mismos [requisitos del sistema](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs) que Visual Studio.  

### <a name="available-languages---ssdt-for-vs-2017"></a>Idiomas disponibles: SSDT para VS 2017

Esta versión de **SSDT para VS 2017** puede instalarse en los idiomas siguientes:  

[Chino (simplificado)]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x804) | 
[Chino (tradicional)]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x404) | 
[Inglés (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x409) | 
[Francés]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x40c)  
[Alemán]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x410) | 
[Japonés]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x412) | 
[Portugués (Brasil)]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x416) | 
[Ruso]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x419) | 
[Español]( https://go.microsoft.com/fwlink/?linkid=2024393&clcid=0x40a)  


## <a name="offline-install"></a>Instalación sin conexión

Para instalar SSDT cuando no esté conectado a Internet, siga los pasos de esta sección. Para más información, consulte [Creación de una instalación de red de Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio).

En primer lugar, complete los siguientes pasos en línea:

1. [Descargue el instalador independiente de SSDT](#ssdt-for-vs-2017-standalone-installer).
2. [Descargue vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe).
3. Mientras sigue en línea, ejecute uno de los siguientes comandos para descargar todos los archivos necesarios para la instalación sin conexión. Con la opción `--layout` como clave, descarga los archivos reales para la instalación sin conexión. Reemplace <filepath> por el diseño en trazado real para guardar los archivos.

   
   A.   Para un idioma específico, pase la configuración regional: `vs_sql.exe --layout c:\<filepath> --lang en-us` (un solo lenguaje es ~ 1 GB).  
   B. Para todos los idiomas, omita el argumento `--lang`: `vs_sql.exe --layout c:\<filepath>` (todos los idiomas son ~3,9 GB).

4. Ejecute `SSDT-Setup-ENU.exe /layout c:\<filepath>` para extraer la carga SSDT en la misma ubicación `<filepath>` donde se han descargado los archivos de VS2017. Esto garantiza que todos los archivos de ambas se combinen en una única carpeta de diseños.

Después de completar los pasos anteriores, se puede realizar lo siguiente mientras se está sin conexión:

1. Ejecute `vs_setup.exe --NoWeb` para instalar el shell de VS2017 y un proyecto de datos de SQL Server.
2. Desde la carpeta de diseños, ejecute `SSDT-Setup-ENU.exe /install` y seleccione SSIS/SSRS/SSAS.

   - O, si se trata de una instalación desatendida, ejecute `SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive`.  

Para ver las opciones disponibles, ejecute `SSDT-Setup-ENU.exe /help`.

## <a name="supported-sql-versions"></a>Versiones de SQL admitidas
  
|Plantillas de proyecto|Plataformas SQL compatibles|  
|-------------------|--------------------|  
Bases de datos relacionales|  SQL Server 2005* - SQL Server 2017<br> (use SSDT 17.x o SSDT para Visual Studio 2017 para conectarse a [SQL Server en Linux](../linux/sql-server-linux-overview.md))<br /><br />Base de datos SQL de Azure<br /><br />Azure SQL Data Warehouse (solo admite consultas, todavía no se admiten proyectos de base de datos)<br /><br />  * La compatibilidad con SQL Server 2005 está en desuso,<br /><br /> Cambie a una versión de SQL oficialmente compatible.|
  |Modelos de Analysis Services<br /><br />Informes de Reporting Services | SQL Server 2008 - SQL Server 2017|
  |paquetes de Integration Services| SQL Server 2012 - SQL Server 2017    |
  
## <a name="dacfx"></a>DacFx
Tanto en SSDT para Visual Studio 2015 como en SSDT para Visual Studio 2017 se usa DacFx 17.4.1: [Descargar Marco de trabajo de la aplicación de capa de datos de Microsoft® SQL Server® (17.4.1 GA DacFx)](https://www.microsoft.com/download/details.aspx?id=56508).

## <a name="previous-versions"></a>Versiones anteriores

Para descargar e instalar SSDT para Visual Studio 2015 o una versión anterior de SSDT, vea [Versiones anteriores de SQL Server Data Tools (SSDT y SSDT-BI)](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md).



## <a name="next-steps"></a>Pasos siguientes  
Después de instalar SSDT, siga estos tutoriales para aprender a crear bases de datos, paquetes, modelos de datos e informes mediante SSDT:  

- [Desarrollo de bases de datos sin conexión orientado a proyectos](project-oriented-offline-database-development.md)  
- [Tutorial de SSIS: Crear un paquete ETL sencillo](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Tutoriales de Analysis Services (SSAS)](../analysis-services/analysis-services-tutorials-ssas.md)  
- [Crear un informe de tabla básico (Tutorial de SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]


## <a name="see-also"></a>Ver también  
[Foro MSDN de SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog del equipo de SSDT](http://blogs.msdn.com/b/ssdt/)  
[Referencia de la API de DACFx](https://msdn.microsoft.com/library/dn645454.aspx)  
[Descarga de SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
