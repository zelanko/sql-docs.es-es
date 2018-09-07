---
title: Descargar SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 07/02/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- instalar ssdt, descargar ssdt, ssdt más reciente
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 6989aaf0ccef6a9cb7656a23ffdc28062a33839b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43084934"
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

[![descargar](../ssdt/media/download.png) Descargar SSDT para Visual Studio 2017 (15.7.1) ](https://go.microsoft.com/fwlink/?linkid=875613) 

> [!IMPORTANT]
> - Antes de instalar SSDT para Visual Studio 2017 (15.7.1), desinstale las extensiones *Proyectos de Analysis Services* y *Proyectos de Reporting Services*, si ya están instaladas y cierre todas las instancias de VS.
> - Cuando instale SSDT en Windows 10 y elija **Instalar la nueva instancia de SQL Server Data Tools para Visual Studio 2017**, desactive todas las casillas de verificación e instale primero la instancia nueva. Después de instalarla, reinicie el equipo y abra nuevamente el instalador de SSDT para continuar la instalación.  



**Información de versión**  
  
Número de versión: 15.7.1  
Número de compilación: 14.0.16167.0  
Fecha de publicación: 02 de julio de 2018  

Para ver la lista completa de cambios, consulte el [registro de cambios](changelog-for-sql-server-data-tools-ssdt.md).

SSDT para Visual Studio 2017 tiene los mismos [requisitos del sistema](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs) que Visual Studio.  

### <a name="available-languages---ssdt-for-vs-2017"></a>Idiomas disponibles: SSDT para VS 2017

Esta versión de **SSDT para VS 2017** puede instalarse en los idiomas siguientes:  

[Chino (simplificado)]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x804) | 
[Chino (tradicional)]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x404) | 
[Inglés (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x409) | 
[Francés]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x40c)  
[Alemán]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x410) | 
[Japonés]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x412) | 
[Portugués (Brasil)]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x416) | 
[Ruso]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x419) | 
[Español]( https://go.microsoft.com/fwlink/?linkid=875613&clcid=0x40a)  



## <a name="ssdt-for-vs-2015-standalone-installer"></a>SSDT para VS 2015 (instalador independiente)

[![descargar](../ssdt/media/download.png) Descargar SSDT para Visual Studio 2015 (17.4)](https://go.microsoft.com/fwlink/?linkid=863440)

**Información de versión**  
  
Número de versión: 17.4

Número de compilación de esta versión: 14.0.61712.050
  
Para ver la lista completa de cambios, consulte el [registro de cambios](changelog-for-sql-server-data-tools-ssdt.md).

### <a name="available-languages---ssdt-for-vs-2015"></a>Idiomas disponibles: SSDT para VS 2015
  
Esta versión de **SSDT para VS 2015** puede instalarse en los idiomas siguientes:  

[Chino (simplificado)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x804) | 
[Chino (tradicional)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x404) | 
[Inglés (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x409) | 
[Francés]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x40c)  
[Alemán]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x410) | 
[Japonés]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x412) | 
[Portugués (Brasil)]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x416) | 
[Ruso]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x419) | 
[Español]( https://go.microsoft.com/fwlink/?linkid=863440&clcid=0x40a)  

### <a name="iso-images---ssdt-for-vs-2015"></a>Imágenes ISO: SSDT para VS 2015

Una imagen ISO de SSDT puede usarse como forma alternativa de instalar SSDT o configurar un punto de instalación administrativa. ISO es un archivo autocontenido que contiene todos los componentes que necesita SSDT y puede descargarse con un administrador de descargas reiniciable, útil en situaciones con ancho de banda de red limitado o menos confiable. Una vez descargado, el ISO puede montarse como una unidad o copiarse en un DVD.

> [!NOTE]
> Las imágenes ISO de SSDT para VS 2015 17.4 ya están disponibles.

[Chino (simplificado)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x804) |
[Chino (tradicional)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x404) |
[Inglés (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x409) |
[Francés]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x40c)  
[Alemán]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x407) |
[Italiano]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x410) |
[Japonés]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x411) |
[Coreano]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x412) |
[Portugués (Brasil)]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x416) |
[Ruso]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x419) |
[Español]( https://go.microsoft.com/fwlink/?linkid=863443&clcid=0x40a)



## <a name="supported-sql-versions"></a>Versiones de SQL admitidas
  
|Plantillas de proyecto|Plataformas SQL compatibles|  
|-------------------|--------------------|  
Bases de datos relacionales|  SQL Server 2005* - SQL Server 2017<br> (use SSDT 17.x o SSDT para Visual Studio 2017 para conectarse a [SQL Server en Linux](../linux/sql-server-linux-overview.md))<br /><br />Base de datos SQL de Azure<br /><br />Azure SQL Data Warehouse (solo admite consultas, todavía no se admiten proyectos de base de datos)<br /><br />  * La compatibilidad con SQL Server 2005 está en desuso,<br /><br /> Cambie a una versión de SQL oficialmente compatible.|
  |Modelos de Analysis Services<br /><br />Informes de Reporting Services | SQL Server 2008 - SQL Server 2017|
  |paquetes de Integration Services| SQL Server 2012 - SQL Server 2017    |
  
## <a name="dacfx"></a>DacFx
Tanto en SSDT para Visual Studio 2015 como en SSDT para Visual Studio 2017 se usa DacFx 17.4.1: [Descargar Marco de trabajo de la aplicación de capa de datos de Microsoft® SQL Server® (17.4.1 GA DacFx)](https://www.microsoft.com/download/details.aspx?id=56508).


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
