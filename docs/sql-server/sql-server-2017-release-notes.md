---
title: "Notas de la versión de SQL Server 2017 | Microsoft Docs"
ms.custom: 
ms.date: 10/30/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 69f0db3da6a75c64aa331a0050be39274e01dad3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-2017-release-notes"></a>Notas de la versión de SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)] En este artículo se describen las limitaciones y los problemas de SQL Server 2017. Para obtener información relacionada, consulte estos artículos:
- [Novedades de SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)
- [Notas de la versión de SQL Server en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-release-notes)
- [Actualizaciones acumulativas de SQL Server 2017](http://aka.ms/sql2017cu) para más información sobre la versión de la última actualización acumulativa (CU)

**Probar SQL Server**
- [![Descargar desde el Centro de evaluación](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) [Descargar SQL Server 2017](http://go.microsoft.com/fwlink/?LinkID=829477)
- [![Creación de una máquina virtual](../includes/media/azure-vm.png)](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) [Poner en marcha una máquina virtual con SQL Server 2017](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)

## <a name="sql-server-2017---general-availability-release-october-2017"></a>SQL Server de 2017: versión de disponibilidad general (octubre de 2017)
### <a name="database-engine"></a>Motor de base de datos

- **Problema e impacto en el cliente:** después de la actualización, el recurso compartido de red FILESTREAM puede dejar de estar disponible.

- **Solución alternativa:** en primer lugar, reinicie el equipo y compruebe si el recurso compartido de red FILESTREAM está disponible. Si el recurso compartido aún no está disponible, realice los siguientes pasos:

    1. En el Administrador de configuración de SQL Server, haga clic con el botón derecho en la instancia de SQL Server y haga clic en **Propiedades**. 
    2. En la pestaña **FILESTREAM**, dedsactive **Habilitar FILESTREAM para el acceso de transmisión por secuencias de E/S de archivos** y después haga clic en **Aplicar**.
    3. Seleccione **Habilitar FILESTREAM para el acceso de transmisión por secuencias de E/S de archivos** de nuevo con el nombre del recurso compartido original y haga clic en **Aplicar**.

### <a name="master-data-services-mds"></a>Master Data Services (MDS)
- **Problema e impacto en el cliente:** en la página de permisos de usuario, al conceder permisos al nivel de raíz en la vista de árbol de entidades, verá el siguiente error: `"The model permission cannot be saved. The object guid is not valid"`.

- **Soluciones alternativas:** 
  - Conceda permisos a los subnodos en la vista de árbol en lugar de a nivel de raíz.
  - o bien
  - Ejecute el script descrito en el blog del equipo de MDS sobre el [error al aplicar los permisos en el nivel de entidad](http://sqlblog.com/blogs/mds_team/archive/2017/09/05/sql-server-2016-sp1-cu4-regression-error-while-applying-permission-on-entity-level-quick-workaround.aspx).

### <a name="analysis-services"></a>Analysis Services
- **Problema e impacto sobre el cliente:** los conectores de datos de los siguientes orígenes aún no están disponibles para los modelos tabulares en el nivel de compatibilidad 1400.
  - Amazon Redshift
  - IBM Netezza
  - Impala
- **Solución alternativa** : ninguna.   

- **Problema e impacto en el cliente:** los modelos de DirectQuery con el nivel de compatibilidad 1400 con perspectivas pueden generar errores al consultar o detectar metadatos.
- **Solución alternativa:** elimine las perspectivas y vuelva a implementar.

### <a name="tools"></a>Herramientas
- **Problema e impacto en el cliente:** la ejecución de *DReplay* genera un error con el siguiente mensaje: "Error DReplay Unexpected error occurred!" (Error inesperado de DReplay).
- **Solución alternativa** : ninguna.

![barra_horizontal](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-release-candidate-rc2---august-2017"></a>SQL Server 2017 Release Candidate (RC2: agosto de 2017)
No hay notas de la versión de SQL Server en Windows relacionadas con esta versión. Consulte [Notas de la versión de SQL Server 2017 en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-release-notes).


![barra_horizontal](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 Release Candidate (RC1, julio de 2017)
### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SQL Server Integration Services (SSIS) (RC1, julio de 2017)
- **Problema e impacto en el cliente:** se ha cambiado el nombre del parámetro *runincluster* del procedimiento almacenado **[catálogo].[create_execution]** a *runinscaleout* para mejorar la coherencia y la legibilidad.
- **Solución alternativa:** si tiene scripts existentes para ejecutar paquetes en Escalabilidad horizontal, debe cambiar el nombre del parámetro de *runincluster* a *runinscaleout* para que los scripts funcionen en RC1.

- **Problema e impacto en el cliente:** SQL Server Management Studio (SSMS) 17.1 y versiones anteriores no pueden desencadenar la ejecución de paquetes en Escalabilidad horizontal en RC1. El mensaje de error es este: "*@runincluster* no es un parámetro para el procedimiento **create_execution**". Este problema se corrige en la versión siguiente de SSMS, la versión 17.2. La versión 17.2 y versiones posteriores de SSMS admiten el nuevo nombre de parámetro y la ejecución de paquetes en Escalabilidad horizontal. 
- **Solución alternativa:** hasta que esté disponible la versión 17.2 de SSMS:
  1. Utilice la versión existente de SSMS para generar el script de ejecución de paquetes.
  2. En el script, cambie el nombre del parámetro *runincluster* a *runinscaleout*.
  3. Ejecute el script.

![barra_horizontal](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1 (mayo de 2017)
### <a name="documentation-ctp-21"></a>Documentación (CTP 2.1)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **Problema e impacto sobre el cliente:** si tiene SQL Server Reporting Services y Power BI Report Server en el mismo equipo y desinstala uno de ellos, no podrá conectarse al servidor de informes que quede con el Administrador de configuración del servidor de informes.
- **Solución alternativa:** para solucionar este problema, debe realizar las siguientes operaciones después de desinstalar uno de los servidores.

    1. Inicie un símbolo del sistema en modo de administrador.
    2. Vaya al directorio donde está instalado el servidor de informes restante.

        *Ubicación predeterminada del servidor de informes de Power BI: C:\Archivos de programa\Servidor de informes de Microsoft Power BI*

        *Ubicación predeterminada de SQL Server Reporting Services: C:\Archivos de programa\Microsoft SQL Server Reporting Services*

    3. Después, vaya a la siguiente carpeta, que puede ser *SSRS* o *PBIRS*, en función del servidor que quede.
    4. Vaya a la carpeta WMI.
    5. Ejecute el siguiente comando:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Si ve el error siguiente, ignórelo.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **Problema e impacto en el cliente:** después de realizar la instalación en un equipo que tenga una versión 2016 de *TSqlLanguageService.msi* (mediante el programa de instalación de SQL o como un paquete redistribuible independiente), se quitan las versiones v13.* (SQL 2016) de *Microsoft.SqlServer.Management.SqlParser.dll* y *Microsoft.SqlServer.Management.SystemMetadataProvider.dll*. Todas las aplicaciones que tengan una dependencia en las versiones 2016 de dichos ensamblados dejarán de funcionar y se producirá un error similar a este: *Error: No se puede cargar el archivo o ensamblado 'Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' ni una de sus dependencias. El sistema no encuentra el archivo especificado.*

   Además, se producirá un error si trata de volver a instalar una versión 2016 de TSqlLanguageService.msi y aparecerá el mensaje: *No se pudo instalar Servicio de lenguaje T-SQL de Microsoft SQL Server 2016 porque ya existe una versión superior en el equipo*.

- **Solución alternativa:** para solucionar este problema y corregir una aplicación que depende de la versión v13 de los ensamblados, siga estos pasos:

   1. Vaya a **Agregar o quitar programas**.
   2. Busque *Servicio de lenguaje T-SQL de Microsoft SQL Server vNext CTP2.1*, haga clic en él con el botón derecho y seleccione **Desinstalar**.
   3. Después de quitar el componente, repare la aplicación que se interrumpe o vuelva a instalar la versión adecuada de *TSqlLanguageService.MSI*.

   Esta solución quitará la versión v14 de esos ensamblados, por lo que dejarán de funcionar todas las aplicaciones que dependan de las versiones v14. Si se necesitan esos ensamblados, es necesario realizar una instalación independiente sin ninguna instalación en paralelo de 2016.

![barra_horizontal](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0 (abril 2017)
### <a name="documentation-ctp-20"></a>Documentación (CTP 2.0)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="always-on-availability-groups"></a>Grupos de disponibilidad AlwaysOn

- **Problema e impacto en el usuario:** una instancia de SQL Server que hospeda una réplica secundaria del grupo de disponibilidad se bloquea si la versión principal de SQL Server es inferior a la instancia que hospeda la réplica principal. Afecta a las actualizaciones de todas las versiones compatibles de SQL Server que hospedan grupos de disponibilidad para SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0. Este problema se produce en las siguientes circunstancias. 

> 1. El usuario actualiza la réplica secundaria que hospeda la instancia de SQL Server de acuerdo con los [procedimientos recomendados](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).
> 2. Después de actualizar, se produce una conmutación por error y la réplica secundaria que se acaba de actualizar se convierte en la principal antes de completar la actualización de todas las réplicas secundarias del grupo de disponibilidad. La réplica principal anterior es ahora una réplica secundaria que tiene una versión anterior a la principal.
> 3. El grupo de disponibilidad está en una configuración no admitida y las réplicas secundarias restantes pueden ser vulnerables a los bloqueos. 

- **Solución alternativa:** conéctese a la instancia de SQL Server que hospeda la nueva réplica principal y quite la réplica secundaria errónea de la configuración.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   La instancia de SQL Server que hospedaba la réplica secundaria se recupera.

## <a name="more-information"></a>Más información
- [notas de la versión de SQL Server Reporting Services](../reporting-services/reporting-services-release-notes.md).
- [Problemas conocidos de Machine Learning Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
- [Vínculos e información del Centro de actualizaciones de SQL Server sobre todas las versiones compatibles](https://msdn.microsoft.com/library/ff803383.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
