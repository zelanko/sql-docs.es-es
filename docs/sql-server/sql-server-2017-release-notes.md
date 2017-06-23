---
title: "Notas de la versión SQL Server de 2017 | Documentos de Microsoft"
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 67c1c0f3a9da6cc5d050da5db8a493f5da934c2a
ms.openlocfilehash: fa45fea4ebb378f035b4b4af2b1fa8a20bc152a5
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-2017-release-notes"></a>Notas de la versión SQL Server de 2017
En este tema se describen las limitaciones y los problemas de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]. Para obtener información relacionada, vea lo siguiente:

- [Novedades en SQL Server de 2017](../sql-server/what-s-new-in-sql-server-2017.md).
- [SQL Server en las notas de la versión de Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes).
- [Notas de la versión de SQL Server Reporting Services](../reporting-services/reporting-services-release-notes.md).

 **Pruébelo:**    
   -   [![Descargar desde el Centro de evaluación](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  Descargar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] desde el **[Centro de evaluación](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-ctp-21-may--2017"></a>CTP de SQL Server de 2017 2.1 (mayo de 2017)
### <a name="documentation-ctp-21"></a>Documentación (CTP 2.1)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **Problema e impacto:** si tiene SQL Server Reporting Services y Power de servidor de informes BI en el mismo equipo y desinstalar uno de ellos, ya no podrá conectarse al servidor de informes con el Administrador de configuración del servidor de informes restantes.
- **Solución alternativa** para solucionar este problema, debe realizar las siguientes operaciones después de desinstalar uno de los servidores.

    1. Inicie un símbolo del sistema en modo de administrador.
    2. Vaya al directorio donde está instalado el servidor de informes restantes.

        *Ubicación predeterminada de servidor de informes de Power BI: servidor de informes de C:\Program Files\Microsoft Power BI*

        *Ubicación predeterminada de SQL Server Reporting Services: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. A continuación, vaya a la carpeta siguiente. Esto será *SSRS* o *PBIRS* según lo que queda.
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

- **Problema e impacto:** después de instalar en un equipo que tenga una versión de 2016 *TSqlLanguageService.msi* (mediante el programa de instalación de SQL o como un paquete redistribuible independiente) la v13.* (SQL 2016) versiones instaladas de *Microsoft.SqlServer.Management.SqlParser.dll* y *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* se quitan. Todas las aplicaciones que tienen una dependencia en las versiones de 2016 de dichos ensamblados, a continuación, dejarán de funcionar, dando a un error similar al: *error: no se pudo cargar el archivo o ensamblado ' Microsoft.SqlServer.Management.SqlParser, Version = 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91' o uno de sus dependencias. El sistema no encuentra el archivo especificado.*

   Además, se producirá un error si intenta volver a instalar una versión de TSqlLanguageService.msi 2016 con el mensaje: *error de instalación del servicio Microsoft SQL Server 2016 T-SQL lenguaje porque ya existe una versión posterior en el equipo*.

- **Solución alternativa** para solucionar este problema y corregir una aplicación que depende de la versión 13 versión de los ensamblados siga estos pasos:

   1. Vaya a **agregar o quitar programas**
   1. Buscar *Microsoft SQL Server vNext CTP2.1 de servicio de lenguaje T-SQL*, haga clic en él y seleccione **desinstalar**.
   1. Después de quita el componente, reparar la aplicación que se interrumpe (o volver a instalar la versión adecuada de *TSqlLanguageService.MSI*)

   Esta solución quitará la versión v14 de dichos ensamblados, por lo que todas las aplicaciones que dependen de las versiones de v14 dejará de funcionar. Si se necesitan esos ensamblados, a continuación, es necesaria una instalación independiente sin ningún 2016 instala side-by-side.

![barra_horizontal](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>2017 CTP 2.0 (abril de 2017) de SQL Server
### <a name="documentation-ctp-20"></a>Documentación (CTP 2.0)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="always-on-availability-groups"></a>Grupos de disponibilidad AlwaysOn

- **Problema e impacto:** instancia A SQL Server que hospeda una réplica secundaria del grupo de disponibilidad se bloquea si la versión principal de SQL Server es inferior a la instancia que hospeda la réplica principal. Afecta a las actualizaciones de todas las versiones compatibles de SQL Server que hospedan los grupos de disponibilidad para SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0. Esto sucede en los pasos siguientes. 

> 1. Usuario actualiza la réplica secundaria de SQL Server instancia hospedaje de acuerdo con [prácticas recomendadas](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).
> 2. Después de actualizar, se produce una conmutación por error y secundario recién actualizado se convierte en principal antes de completar la actualización para todas las réplicas secundarias del grupo de disponibilidad. El elemento principal anterior es ahora una base de datos secundaria que es una versión anterior a la principal.
> 3. El grupo de disponibilidad está en una configuración no admitida y las restantes réplicas secundarias pueden ser vulnerables a los bloqueos. 

- **Solución alternativa** conectar a la instancia de SQL Server que hospeda la nueva réplica principal y quite la réplica secundaria defectuosa de la configuración.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   Recupera la instancia de SQL Server que hospeda la réplica secundaria.


![barra_horizontal](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-14-march--2017"></a>Versión de CTP de SQL Server de 2017 1.4 (marzo de 2017)

### <a name="documentation-ctp-14"></a>Documentación (CTP 1.4)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

![barra_horizontal](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-13-february--2017"></a>Versión de CTP de SQL Server de 2017 1.3 (febrero de 2017)
### <a name="supported-installation-scenarios-ctp-13"></a>Escenarios de instalación compatibles (CTP 1.3)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] está pensado únicamente como versión de prueba.  No se admiten las implementaciones de producción. Se recomienda instalar y probar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] en una máquina virtual.

### <a name="documentation-ctp-13"></a>Documentación (CTP 1.3)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SQL Server Integration Services (SSIS) (CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>No se admiten componentes de CDC en esta versión de CTP
-   **Problema e impacto en el cliente**: Tarea Control CDC, Origen de CDC y Divisor CDC no son compatibles en esta versión de CTP.
-   **Solución:**no hay solución alguna.


![barra_horizontal](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-12-january--2017"></a>Versión de CTP de SQL Server de 2017 1.2 (enero de 2017)
### <a name="supported-installation-scenarios-ctp-12"></a>Escenarios de instalación compatibles (CTP 1.2)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] está pensado únicamente como versión de prueba.  No se admiten las implementaciones de producción. Se recomienda instalar y probar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] en una máquina virtual.

### <a name="sql-server-database-engine-ctp-12"></a>Motor de base de datos de SQL Server (CTP 1.2)
- **Problema e impacto en el cliente:** en algunos casos, el servicio MSSQLSERVER se atascará en el estado "Iniciándose".
- **Solución alternativa:** para evitar este problema:
  -  Cree una dependencia entre el servicio `mssqlserver` y el servicio `keyiso` . Una forma de hacerlo es ejecutar lo siguiente desde un símbolo del sistema con privilegios elevados: `sc config mssqlserver depend= keyiso`
  - Reinicie el equipo.

### <a name="documentation-ctp-12"></a>Documentación (CTP 1.2)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] .  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a:**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SQL Server Integration Services (SSIS) (CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>Puede producirse un error al eliminar el catálogo de SSIS si está instalado el escalado horizontal de SSIS
**Problema e impacto en el cliente:**cuando la característica de escalado de SSIS está instalada en un equipo, la eliminación de la base de datos del catálogo de SSISDB puede producir el siguiente error: "No se pudo quitar el inicio de sesión *'inicio de sesión'* . El usuario tiene una sesión iniciada".
   
**Solución**:
-   En un equipo maestro de escalado horizontal, ejecute el comando "services.msc" para abrir la ventana Servicios. Detenga el servicio SQL Server Integration Services Cluster Master.
-   En equipos de trabajador de escalado horizontal que se conectan al maestro, ejecute el comando "services.msc" para abrir la ventana Servicios. Detenga el servicio SQL Server Integration Services Cluster Worker.

Ahora puede eliminar la base de datos del catálogo de SSISDB.

### <a name="sql-server-master-data-services-ctp-12"></a>SQL Server Master Data Services (CTP 1.2)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>Puede que una transacción no funcione si el tipo de registro de transacción de entidad está establecido en atributo
**Problema e impacto en el cliente:** cuando el tipo de registro de transacción de entidad está establecido en **Atributo** en [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] (el valor predeterminado es **Miembro**), se producirá un error en los siguientes escenarios:

* Las transacciones de cambios de entidad no se muestran en el sitio web.
* No se puede abrir la página **Transacciones** en el sitio web e invertir una transacción.
* No se puede actualizar una entidad con una anotación de transacción en el sitio web.

**Solución:**no hay solución alguna.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Es posible que la copia de la versión no funcione si **Copiar solo la versión confirmada** está establecido en false.
-  **Problema e impacto en el cliente:** cuando la opción **Copiar solo la versión confirmada** está establecida en **No** (el valor predeterminado es **Sí**), puede producirse un error en la operación de copia de la versión. No hay ningún mensaje de error.
-  **Solución:**no hay solución alguna.

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Comunicación con el equipo de ingeniería de SQL Server 
- [Stack Overflow en español (etiqueta sql server): preguntas técnicas](http://stackoverflow.com/questions/tagged/sql-server)
- [Foros de MSDN: preguntas técnicas](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: informar sobre errores y solicitar características](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: debate general sobre R](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)


