---
title: Descargar SQL Server Data Tools (SSDT) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssdt
ms.topic: conceptual
keywords: instalar ssdt, descargar ssdt, ssdt más reciente
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 08/15/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: a79940fa5696a65ed580d8550984d090a48eebdf
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72807445"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>Descargar e instalar SQL Server Data Tools (SSDT) para Visual Studio

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**SQL Server Data Tools** es una herramienta de desarrollo moderna para crear bases de datos relacionales de SQL Server, bases de datos SQL de Azure, modelos de datos de Analysis Services (AS), paquetes de Integration Services (IS) e informes de Reporting Services (RS). Gracias a SSDT, puede diseñar e implementar cualquier tipo de contenido de SQL Server con la misma facilidad con la que desarrollaría una aplicación en Visual Studio.

## <a name="changes-in-ssdt-for-visual-studio-2019"></a>Cambios en SSDT para Visual Studio 2019

Con Visual Studio 2019, la funcionalidad necesaria para habilitar Analysis Services, Integration Services y los proyectos de Reporting Services se ha trasladado a las respectivas extensiones de Visual Studio. La funcionalidad central de SSDT para crear proyectos de base de datos sigue siendo una parte integral a Visual Studio (necesita el almacenamiento de datos y la carga de trabajo de procesamiento durante la instalación). No se requiere más instalación de SSDT independiente.

Si ya tiene una licencia para Visual Studio 2019:

- Para proyectos de SQL Database, instale el almacenamiento de datos y la carga de procesamiento para Visual Studio
- Para proyectos de Analysis Services, Integration Services o Reporting Services, instale las [extensiones](https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions) adecuadas de Marketplace.

Si aún no tiene una licencia para Visual Studio 2019:

- Instalación de [Visual Studio Community 2019](https://visualstudio.microsoft.com/downloads/)
- Instale las [extensiones](https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions) de Analysis Services, Integration Services o Reporting Services, según corresponda.

## <a name="changes-in-ssdt-for-visual-studio-2017"></a>Cambios en SSDT para Visual Studio 2017

A partir de Visual Studio 2017, se ha integrado la funcionalidad de creación de proyectos de base de datos en la instalación de Visual Studio. No hay ninguna necesidad de instalar al instalador independiente de SSDT para la experiencia SSDT básica. Para crear proyectos de Integration Services, Analysis Services o Reporting Services aún necesita el instalador independiente de SSDT.

- Para proyectos de base de datos, instale el almacenamiento de datos y la carga de procesamiento para Visual Studio.
- Para proyectos de Analysis Services, Integration Services o Reporting Services, descargue e instale [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017).

## <a name="install-ssdt-with-visual-studio-2017"></a>Instalar SSDT con Visual Studio 2017

Para instalar SSDT durante la [instalación de Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio), seleccione la carga de trabajo **Procesamiento y almacenamiento de datos** y, después, seleccione **SQL Server Data Tools**. Si Visual Studio ya está instalado, puede [modificar la lista de cargas de trabajo](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) para incluir SSDT: ![Carga de trabajo de procesamiento y almacenamiento de datos](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)

## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Instalar las herramientas de Analysis Services, Integration Services y Reporting Services

Para instalar la compatibilidad con proyectos de AS, IS y RS, ejecute el [instalador independiente de SSDT](#ssdt-for-vs-2017-standalone-installer).

El instalador enumera las instancias disponibles de Visual Studio a las que se van a agregar las herramientas de SSDT. Si Visual Studio no está instalado, al seleccionar **Instalar una nueva instancia de SQL Server Data Tools** se instala SSDT con una versión mínima de Visual Studio, pero para una mejor experiencia se recomienda usar SSDT con [la versión más reciente de Visual Studio](https://www.visualstudio.com/downloads).

![Selección de AS, IS, RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)

## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT para VS 2017 (instalador independiente)

[![descargar](../ssdt/media/download.png) Descargar SSDT para Visual Studio 2017 (15.9.2)](https://go.microsoft.com/fwlink/?linkid=2095463)

> [!IMPORTANT]
> - Antes de instalar SSDT para Visual Studio 2017 (15.9.2), desinstale las extensiones *Proyectos de Analysis Services* y *Proyectos de Reporting Services*, si están instaladas, y cierre todas las instancias de VS.
> - Use SSDT para Visual Studio 2017 (15.8.0) o anterior, para diseñar paquetes SSIS que contengan orígenes y destinos de Teradata. SSDT para Visual Studio 2017 después de 15.8.0 no puede diseñar paquetes SSIS que contengan orígenes y destinos de Teradata de Attunity.

### <a name="version-information"></a>Información de versión

Número de versión: 15.9.2 Número de compilación: 14.0.16194.0 Fecha de publicación: 17 de julio de 2019 

Para ver una lista completa de cambios, consulte las [notas de la versión de SQL Server Data Tools (SSDT)](release-notes-ssdt.md).

SSDT para Visual Studio 2017 tiene los mismos [requisitos del sistema](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs) que Visual Studio.

### <a name="available-languages---ssdt-for-vs-2017"></a>Idiomas disponibles: SSDT para VS 2017

Esta versión de **SSDT para VS 2017** puede instalarse en los idiomas siguientes:

- [Chino (simplificado)]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x804)
- [Chino (tradicional)]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x404)
- [Inglés (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x409)
- [Francés]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x40c)
- [Alemán]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x407)
- [Italiano]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x410)
- [Japonés]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x411)
- [Coreano]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x412)
- [Portugués (Brasil)]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x416)
- [Ruso]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x419)
- [Español]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x40a)

## <a name="offline-install"></a>Instalación sin conexión

Para instalar SSDT cuando no esté conectado a Internet, siga los pasos de esta sección. Para más información, consulte [Creación de una instalación de red de Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio).

En primer lugar, complete los siguientes pasos **en línea**:

1. [Descargue el instalador independiente de SSDT](#ssdt-for-vs-2017-standalone-installer).
2. [Descargue vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe).
3. Mientras sigue en línea, ejecute uno de los siguientes comandos para descargar todos los archivos necesarios para la instalación sin conexión. Con la opción `--layout` como clave, descarga los archivos reales para la instalación sin conexión. Reemplace `<filepath>` por el diseño en trazado real para guardar los archivos.
   1. Para un idioma específico, pase la configuración regional: `vs_sql.exe --layout c:\<filepath> --lang en-us` (un solo lenguaje es ~ 1 GB).
   1. Para todos los idiomas, omita el argumento `--lang`: `vs_sql.exe --layout c:\<filepath>` (todos los idiomas son ~3,9 GB).

4. Ejecute `SSDT-Setup-ENU.exe /layout c:\<filepath>` para extraer la carga SSDT en la misma ubicación `<filepath>` donde se han descargado los archivos de VS2017. Esta acción garantiza que todos los archivos de ambas se combinen en una única carpeta de diseños.

Después de completar los pasos anteriores, se pueden realizar los pasos siguientes mientras se está sin **conexión**:

1. Ejecute `vs_setup.exe --NoWeb` para instalar el shell de VS2017 y un proyecto de datos de SQL Server.
2. Desde la carpeta de diseños, ejecute `SSDT-Setup-ENU.exe /install` y seleccione SSIS/SSRS/SSAS.
   - Para una instalación desatendida, ejecute `SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive`.

Para ver las opciones disponibles, ejecute `SSDT-Setup-ENU.exe /help`.

> [!NOTE]
> Si usa una versión completa de Visual Studio 2017, cree una carpeta sin conexión exclusiva para SSDT y ejecute `SSDT-Setup-ENU.exe` desde la carpeta recién creada (no agregue SSDT a otro diseño sin conexión de Visual Studio 2017). Si agrega el diseño SSDT a un diseño sin conexión de Visual Studio existente, no se crearán los componentes de tiempo de ejecución (.exe) necesarios.

### <a name="considerations-and-limitations"></a>Consideraciones y limitaciones

- No es posible instalar sin conexión la versión de comunidad.
- Para actualizar SSDT, debe seguir la misma ruta de acceso que se usa para instalar SSDT. Por ejemplo, si agregó SSDT mediante VSIX, actualice a través de VSIX. Si instaló SSDT a través de una instalación independiente, debe actualizarlo con ese método.

## <a name="supported-sql-versions"></a>Versiones de SQL admitidas
 
|Plantillas de proyecto|Plataformas SQL compatibles| 
|-------------------|--------------------| 
|Bases de datos relacionales| SQL Server 2005\* - SQL Server 2017<br> (use SSDT 17.x o SSDT para Visual Studio 2017 para conectarse a [SQL Server en Linux](../linux/sql-server-linux-overview.md))<br /><br />Base de datos SQL de Azure<br /><br />Azure SQL Data Warehouse (solo admite consultas, todavía no se admiten proyectos de base de datos).<br /><br /> \* Ya no se ofrece soporte técnico para SQL Server 2005.<br /><br /> Cambie a una versión de SQL oficialmente compatible.|
|Modelos de Analysis Services<br /><br />Informes de Reporting Services | SQL Server 2008 - SQL Server 2017|
|paquetes de Integration Services| SQL Server 2012 - SQL Server 2019 |

## <a name="dacfx"></a>DacFx

En SSDT para Visual Studio 2015 y SSDT para Visual Studio 2017 se usa DacFx 17.4.1: [Descargar Data-Tier Application Framework (DacFx) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508).

## <a name="previous-versions"></a>Versiones anteriores

Para descargar e instalar SSDT para Visual Studio 2015 o una versión anterior de SSDT, vea [Versiones anteriores de SQL Server Data Tools (SSDT y SSDT-BI)](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md).

## <a name="next-steps"></a>Pasos siguientes

Después de instalar SSDT, siga estos tutoriales para aprender a crear bases de datos, paquetes, modelos de datos e informes mediante SSDT: 

- [Desarrollo de bases de datos sin conexión orientado a proyectos](project-oriented-offline-database-development.md) 
- [Tutorial de SSIS: Creación de un paquete ETL sencillo](../integration-services/ssis-how-to-create-an-etl-package.md) 
- [Tutoriales de Analysis Services (SSAS)](https://docs.microsoft.com/analysis-services/analysis-services-tutorials-ssas) 
- [Crear un informe de tabla básico (Tutorial de SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) 

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>Consulte también

[Foro MSDN de SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt) 
[Blog del equipo de SSDT](https://blogs.msdn.com/b/ssdt/) 
[Referencia de la API DACFx](https://msdn.microsoft.com/library/dn645454.aspx) 
[Descarga de SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) 
