---
title: "Notas de la versión de SQL Server 2017 | Microsoft Docs"
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 6aa73e749d4f308265dfe27a160802c15a391a3e
ms.openlocfilehash: a2950b6aef0e12653efbb9eb26fd3f1ae6cb951e
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-2017-release-notes"></a>Notas de la versión de SQL Server 2017
En este tema se describen las limitaciones y los problemas de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]. Para obtener información relacionada, consulte lo siguiente:

- [Novedades de SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).
- [notas de la versión de SQL Server en Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes).
- [notas de la versión de SQL Server Reporting Services](../reporting-services/reporting-services-release-notes.md).

 **Pruébelo:**    
   -   [![Descargar desde el Centro de evaluación](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  Descargar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] desde el **[Centro de evaluación](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 Release Candidate (RC1, julio de 2017)

### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SQL Server Integration Services (SSIS) (RC1, julio de 2017)
- **Problema e impacto en el cliente:** se ha cambiado el nombre del parámetro *runincluster* del procedimiento almacenado **[catálogo].[create_execution]** a *runinscaleout* para mejorar la coherencia y la legibilidad.
- **Solución alternativa:** si tiene scripts existentes para ejecutar paquetes en Escalabilidad horizontal, debe cambiar el nombre del parámetro de *runincluster* a *runinscaleout* para que los scripts funcionen en RC1.

- **Problema e impacto en el cliente:** SQL Server Management Studio (SSMS) 17.1 y versiones anteriores no pueden desencadenar la ejecución de paquetes en Escalabilidad horizontal en RC1. El mensaje de error es este: "*@runincluster* no es un parámetro para el procedimiento **create_execution**". Este problema se corrige en la versión siguiente de SSMS, la versión 17.2. La versión 17.2 y versiones posteriores de SSMS admiten el nuevo nombre de parámetro y la ejecución de paquetes en Escalabilidad horizontal. 
- **Solución alternativa:** hasta que esté disponible la versión 17.2 de SSMS, puede usar la versión existente de SSMS para generar el script de ejecución de paquetes, cambiar el nombre del parámetro *runincluster* a *runinscaleout* en el script y, luego, ejecutar el script.

![barra_horizontal](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1 (mayo de 2017)
### <a name="documentation-ctp-21"></a>Documentación (CTP 2.1)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **Problema e impacto en el cliente:** si tiene SQL Server Reporting Services y el servidor de informes de Power BI en el mismo equipo y desinstala uno de ellos, ya no podrá conectarse al servidor de informes que quede con el Administrador de configuración del servidor de informes.
- **Solución alternativa:** para solucionar este problema, debe realizar las siguientes operaciones después de desinstalar uno de los servidores.

    1. Inicie un símbolo del sistema en modo de administrador.
    2. Vaya al directorio donde está instalado el servidor de informes restante.

        *Ubicación predeterminada del servidor de informes de Power BI: C:\Archivos de programa\Servidor de informes de Microsoft Power BI*

        *Ubicación predeterminada de SQL Server Reporting Services: C:\Archivos de programa\Microsoft SQL Server Reporting Services*

    3. Después, vaya a la carpeta siguiente. Esta será *SSRS* o *PBIRS*, en función del servidor que quede.
    4. Vaya a la carpeta WMI.
    5. Ejecute el siguiente comando:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Puede omitir el error siguiente, si lo ve.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **Problema e impacto en el cliente:** después de instalar en un equipo que tenga una versión de 2016 de *TSqlLanguageService.msi* instalada (mediante el programa de instalación de SQL o como un paquete redistribuible independiente) las versiones v13.* (SQL 2016) de *Microsoft.SqlServer.Management.SqlParser.dll* y *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* se quitan. Todas las aplicaciones que tengan una dependencia en las versiones de 2016 de dichos ensamblados dejarán de funcionar, dando lugar a un error similar a este: *Error: No se pudo cargar el archivo o ensamblado 'Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' o una de sus dependencias. El sistema no encuentra el archivo especificado.*

   Además, se producirá un error si intenta volver a instalar una versión de 2016 de TSqlLanguageService.msi y aparecerá el mensaje: *No se pudo instalar Servicio de lenguaje T-SQL de Microsoft SQL Server 2016 porque ya existe una versión superior en este equipo*.

- **Solución alternativa:** para solucionar este problema y corregir una aplicación que depende de la versión v13 de los ensamblados, siga estos pasos:

   1. Vaya a **Agregar o quitar programas**.
   1. Busque *Servicio de lenguaje T-SQL de Microsoft SQL Server vNext CTP2.1*, haga clic en él con el botón derecho y seleccione **Desinstalar**.
   1. Después de quitar el componente, repare la aplicación que se interrumpe (o vuelva a instalar la versión adecuada de *TSqlLanguageService.MSI*).

   Esta solución quitará la versión v14 de esos ensamblados, por lo que dejarán de funcionar todas las aplicaciones que dependan de las versiones de v14. Si se necesitan esos ensamblados, es necesario realizar una instalación independiente sin ninguna instalación en paralelo de 2016.

![barra_horizontal](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0 (abril 2017)
### <a name="documentation-ctp-20"></a>Documentación (CTP 2.0)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="always-on-availability-groups"></a>Grupos de disponibilidad AlwaysOn

- **Problema e impacto en el usuario:** una instancia de SQL Server que hospeda una réplica secundaria del grupo de disponibilidad se bloquea si la versión principal de SQL Server es inferior a la instancia que hospeda la réplica principal. Afecta a las actualizaciones de todas las versiones compatibles de SQL Server que hospedan grupos de disponibilidad para SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0. Esto sucede en los pasos siguientes. 

> 1. El usuario actualiza la réplica secundaria que hospeda la instancia de SQL Server de acuerdo con los [procedimientos recomendados](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).
> 2. Después de actualizar, se produce una conmutación por error y la réplica secundaria que se acaba de actualizar se convierte en la réplica principal antes de completar la actualización de todas las réplicas secundarias del grupo de disponibilidad. La réplica principal anterior es ahora una réplica secundaria que tiene una versión anterior a la principal.
> 3. El grupo de disponibilidad está en una configuración no admitida y las réplicas secundarias restantes pueden ser vulnerables a los bloqueos. 

- **Solución alternativa:** conéctese a la instancia de SQL Server que hospeda la nueva réplica principal y quite la réplica secundaria errónea de la configuración.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   La instancia de SQL Server que hospedaba la réplica secundaria se recupera.

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Comunicación con el equipo de ingeniería de SQL Server 
- [Stack Overflow en español (etiqueta sql server): preguntas técnicas](http://stackoverflow.com/questions/tagged/sql-server)
- [Foros de MSDN: preguntas técnicas](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: informar sobre errores y solicitar características](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: debate general sobre R](https://www.reddit.com/r/SQLServer/)

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
