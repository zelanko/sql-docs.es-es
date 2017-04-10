---
title: "Notas de la versi&#243;n de SQL Server vNext | Microsoft Docs"
ms.custom: ""
ms.date: "03/12/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: "craigg-msft"
ms.author: "craigg"
manager: "jhubbard"
caps.handback.revision: 39
---
# Notas de la versi&#243;n de SQL Server vNext
En este tema se describen las limitaciones y los problemas de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

- Para leer sobre las novedades de esta versión, vea [What's New in SQL Server vNext (Novedades de SQL Server vNext)](../sql-server/what-s-new-in-sql-server-vnext.md).
- Las [notas de la versión de SQL Server en Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes) se publican en nuestra nueva plataforma de documentación en continuo desarrollo.
- Las [notas de la versión de SQL Server Reporting Services](../reporting-services/notas-de-la-versión-de-reporting-services.md) están publicadas en la sección sobre Reporting Services.

 **Pruébelo:**    
   -   [![Descargar desde el Centro de evaluación](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) Descargar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] desde el **[Centro de evaluación](http://go.microsoft.com/fwlink/?LinkID=829477)**


## <a name="sql-server-vnext-ctp-13-february--2017"></a>SQL Server vNext CTP 1.3 (febrero de 2017)
### <a name="supported-installation-scenarios-ctp-13"></a>Escenarios de instalación compatibles (CTP 1.3)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] está pensado únicamente como versión de prueba.  No se admiten las implementaciones de producción. Se recomienda instalar y probar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] en una máquina virtual.

### <a name="documentation-ctp-13"></a>Documentación (CTP 1.3)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)].  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SQL Server Integration Services (SSIS) (CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>No se admiten componentes de CDC en esta versión de CTP
-   **Problema e impacto en el cliente**: Tarea Control CDC, Origen de CDC y Divisor CDC no son compatibles en esta versión de CTP.
-   **Solución:** no hay solución alguna.


![barra_horizontal](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-12-january--2017"></a>SQL Server vNext CTP 1.2 (enero de 2017)
### <a name="supported-installation-scenarios-ctp-12"></a>Escenarios de instalación compatibles (CTP 1.2)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] está pensado únicamente como versión de prueba.  No se admiten las implementaciones de producción. Se recomienda instalar y probar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] en una máquina virtual.

### <a name="sql-server-database-engine-ctp-12"></a>Motor de base de datos de SQL Server (CTP 1.2)
- **Problema e impacto en el cliente:** en algunos casos, el servicio MSSQLSERVER se atascará en el estado "Iniciándose".
- **Solución alternativa:** para evitar este problema:
  -  Cree una dependencia entre el servicio `mssqlserver` y el servicio `keyiso`. Una forma de hacerlo es ejecutar lo siguiente desde un símbolo del sistema con privilegios elevados: `sc config mssqlserver depend= keyiso`
  - Reinicie el equipo.

### <a name="documentation-ctp-12"></a>Documentación (CTP 1.2)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)].  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a:**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SQL Server Integration Services (SSIS) (CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>Puede producirse un error al eliminar el catálogo de SSIS si está instalado el escalado horizontal de SSIS
**Problema e impacto en el cliente:** cuando la característica de escalado de SSIS está instalada en un equipo, la eliminación de la base de datos del catálogo de SSISDB puede producir el siguiente error: "No se pudo quitar el inicio de sesión *'inicio de sesión'*. El usuario tiene una sesión iniciada".
   
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

**Solución:** no hay solución alguna.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Es posible que la copia de la versión no funcione si **Copiar solo la versión confirmada** está establecido en false.
-  **Problema e impacto en el cliente:** cuando la opción **Copiar solo la versión confirmada** está establecida en **No** (el valor predeterminado es **Sí**), puede producirse un error en la operación de copia de la versión. No hay ningún mensaje de error.
-  **Solución:** no hay solución alguna.

![barra_horizontal](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-11-december--2016"></a>SQL Server vNext CTP 1.1 (diciembre de 2016)
### <a name="supported-installation-scenarios-ctp-11"></a>Escenarios de instalación compatibles (CTP 1.1)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] está pensado únicamente como versión de prueba.  No se admiten las implementaciones de producción. Se recomienda instalar y probar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] en una máquina virtual.

Concretamente, aunque los siguientes escenarios pueden funcionarle, no se han probado exhaustivamente y **no** se admiten en [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]:
- Desinstalación de CTP 1.1.
- Instalación en paralelo con cualquier otra versión de SQL Server.
- Actualización desde cualquier versión anterior de SQL Server.
- No hay componentes del Feature Pack de SQL Server disponibles como parte de la instalación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="documentation-ctp-11"></a>Documentación (CTP 1.1)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)].  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a:**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-master-data-services-ctp-11"></a>SQL Server Master Data Services (CTP 1.1)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>Puede que una transacción no funcione si el tipo de registro de transacción de entidad está establecido en atributo
**Problema e impacto en el cliente:** cuando el tipo de registro de transacción de entidad está establecido en **Atributo** en [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] (el valor predeterminado es **Miembro**), se producirá un error en los siguientes escenarios:

* Las transacciones de cambios de entidad no se muestran en el sitio web.
* No se puede abrir la página **Transacciones** en el sitio web e invertir una transacción.
* No se puede actualizar una entidad con una anotación de transacción en el sitio web.

**Solución:** no hay solución alguna.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Es posible que la copia de la versión no funcione si **Copiar solo la versión confirmada** está establecido en false.
-  **Problema e impacto en el cliente:** cuando la opción **Copiar solo la versión confirmada** está establecida en **No** (el valor predeterminado es **Sí**), puede producirse un error en la operación de copia de la versión. No hay ningún mensaje de error.
-  **Solución:** no hay solución alguna.

### <a name="sql-server-integration-services-ssis-ctp-11"></a>SQL Server Integration Services (SSIS) (CTP 1.1)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>Puede producirse un error al eliminar el catálogo de SSIS si está instalado el escalado horizontal de SSIS
**Problema e impacto en el cliente:** cuando la característica de escalado de SSIS está instalada en un equipo, la eliminación de la base de datos del catálogo de SSISDB puede producir el siguiente error: "No se pudo quitar el inicio de sesión *'inicio de sesión'*. El usuario tiene una sesión iniciada".
   
**Solución**:
-   En un equipo maestro de escalado horizontal, ejecute el comando "services.msc" para abrir la ventana Servicios. Detenga el servicio SQL Server Integration Services Cluster Master.
-   En equipos de trabajador de escalado horizontal que se conectan al maestro, ejecute el comando "services.msc" para abrir la ventana Servicios. Detenga el servicio SQL Server Integration Services Cluster Worker.

Ahora puede eliminar la base de datos del catálogo de SSISDB.

#### <a name="odbc-components-are-not-supported-in-this-ctp-release"></a>No se admiten componentes de ODBC en esta versión de CTP
**Problema e impacto en el cliente**: el administrador de conexiones, el origen y el destino de ODBC no se admiten en esta versión de CTP.

**Solución:** no hay solución alguna.

![barra_horizontal](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-10-november-2016"></a>SQL Server vNext CTP 1.0 (noviembre de 2016)
### <a name="supported-installation-scenarios-ctp10"></a>Escenarios de instalación compatibles (CTP&1;.0)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] está pensado únicamente como versión de prueba.  No se admiten las implementaciones de producción. Se recomienda instalar y probar [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] en una máquina virtual.

Concretamente, aunque los siguientes escenarios pueden funcionarle, no se han probado exhaustivamente y **no** se admiten en [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]:
- Desinstalación de CTP 1.0.
- Instalación en paralelo con cualquier otra versión de SQL Server.
- Actualización desde cualquier versión anterior de SQL Server.
- No hay componentes del Feature Pack de SQL Server disponibles como parte de la instalación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="documentation-ctp-10"></a>Documentación (CTP 1.0)
- **Problema e impacto en el cliente:** la documentación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)].  El contenido de los artículos específico de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] se distinguirá con **Se aplica a:**. 
- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-database-engine-ctp-10"></a>Motor de base de datos de SQL Server (CTP 1.0)
-  **Problema e impacto en el cliente:** la función `STRING_AGG` de CTP1 devuelve el tipo LOB como un resultado (por ejemplo, `NVARCHAR(MAX)`). En una futura versión de CTP, este comportamiento podría cambiar y `STRING_AGG` podría devolver `NVARCHAR(4000)` si los valores de entrada no son tipos LOB. Se podría producir un error de desbordamiento si los resultados concatenados no caben en `NVARCHAR(4000)`.

-  **Problema e impacto en el cliente:** evite usar palabras clave no reservadas, como `WITHIN`, como un alias para expresiones `STRING_AGG`. (Por ejemplo, `SELECT Company.Name, STRING_AGG(Product.Name, ',') AS WITHIN FROM TableA;`). En una futura versión de CTP, el token `WITHIN` después de la llamada a `STRING_AGG` podría usarse como parte de la función `STRING_AGG`.

-  **Solución:** evite el uso del alias `WITHIN` o agregue `AS WITHIN` como una especificación de alias con el fin de evitar conflictos con cambios futuros que podrían agregarse a la función `STRING_AGG`.


### <a name="sql-server-integration-services-ctp-10"></a>SQL Server Integration Services (CTP 1.0)
#### <a name="stop-operation-in-ssis-catalog-may-fail"></a>Puede producirse un error en la operación de detención en el catálogo de SSIS
**Problema e impacto en el cliente:** la detención de una operación de [!INCLUDE[ssIS_md](../includes/ssis-md.md)] con [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)] o el procedimiento almacenado catalog.stop_operation puede producir el siguiente error: "Error de .NET Framework durante la ejecución de una rutina definida por el usuario o la adición de 'stop_operation_internal'".

-  **Solución:** abra el Administrador de tareas de Windows. En la pestaña **Procesos**, busque el proceso denominado **ISServerExec** y haga clic en **Finalizar tarea** para terminar el proceso.

#### <a name="create-dump-of-ssis-pacakge-execution-may-fail"></a>Puede producirse un error al crear un volcado de la ejecución de paquetes SSIS
**Problema e impacto en el cliente:** la creación de un volcado para la ejecución de un paquete mediante el procedimiento almacenado catalog.create_execution_dump puede producir el siguiente error: "Error de .NET Framework durante la ejecución de la rutina definida por el usuario o la adición de 'create_execution_dump_internal'".

-  **Solución:** abra el Administrador de tareas de Windows. En la pestaña **Procesos**, busque el proceso denominado **ISServerExec**, haga clic con el botón derecho en el proceso y, luego, haga clic en **Crear archivo de volcado**.

#### <a name="get-perf-counter-of-ssis-package-execution-may-fail"></a>Puede producirse un error al obtener el contador de rendimiento de la ejecución de paquetes SSIS
**Problema e impacto en el cliente:** la consulta de los contadores de rendimiento de [!INCLUDE[ssIS_md](../includes/ssis-md.md)] mediante la función con valores de tabla catalog.dm_execution_performance_counters puede producir el siguiente error: "Error de .NET Framework durante la ejecución de la rutina definida por el usuario o la adición de 'get_execution_perf_counters'".

-  **Solución**: use el Monitor de rendimiento de Windows para supervisar los valores de los contadores de rendimiento directamente. No hay ninguna solución para los contadores de rendimiento para una ejecución de paquetes concreta.

#### <a name="deleting-catalog-may-fail-when-ssis-scale-out-master-is-installed"></a>Puede producirse un error al eliminar el catálogo si el patrón de escalado horizontal de SSIS está instalado
**Problema e impacto en el cliente:** cuando la característica de escalado de [!INCLUDE[ssIS_md](../includes/ssis-md.md)] está instalada en un equipo, la eliminación del catálogo **SSISDB** puede producir el siguiente error: "No se pudo quitar el inicio de sesión '...' porque el usuario tiene iniciada la sesión". 

**Solución**: 
* En un equipo del patrón de escalado horizontal, ejecute el comando "services.msc" para abrir la ventana **Servicios** y detener el servicio **SQL Server Integration Services Cluster Master**. 

* En equipos del trabajador de escalado horizontal, que se conectan al patrón, ejecute el comando "services.msc" para abrir la ventana **Servicios**. Detenga el servicio **SQL Server Integration Services Cluster Worker**. 

Ahora debería poder eliminar el catálogo **SSISDB**.

#### <a name="odbc-connector-in-ssis-is-not-supported"></a>El conector ODBC de SSIS no es compatible
-  **Problema e impacto en el cliente:** el conector ODCB de [!INCLUDE[ssIS_md](../includes/ssis-md.md)] no es compatible.
-  **Solución alternativa:** no existe.

### <a name="sql-server-reporting-services-ctp-10"></a>SQL Server Reporting Services (CTP 1.0)

SQL Server Reporting Services no va a publicar ninguna característica nueva para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].

### <a name="sql-server-master-data-services-ctp-10"></a>SQL Server Master Data Services (CTP 1.0)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>Puede que una transacción no funcione si el tipo de registro de transacción de entidad está establecido en atributo
**Problema e impacto en el cliente:** cuando el tipo de registro de transacción de entidad está establecido en **Atributo** en [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] (el valor predeterminado es **Miembro**), se producirá un error en los siguientes escenarios:

* Las transacciones de cambios de entidad no se muestran en el sitio web.
* No se puede abrir la página **Transacciones** en el sitio web e invertir una transacción.
* No se puede actualizar una entidad con una anotación de transacción en el sitio web.

**Solución:** no hay solución alguna.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Es posible que la copia de la versión no funcione si **Copiar solo la versión confirmada** está establecido en false.
**Problema e impacto en el cliente:** cuando la opción **Copiar solo la versión confirmada** está establecida en **No** (el valor predeterminado es **Sí**), puede producirse un error en la operación de copia de la versión. No hay ningún mensaje de error.

**Solución:** no hay solución alguna.
 
### <a name="sql-server-management-studio-ssms-ctp-10"></a>SQL Server Management Studio (SSMS) (CTP 1.0)
SQL Server Management Studio es una descarga independiente.  Para obtener la información más reciente, vea [SQL Server Management Studio: notas de la versión](https://msdn.microsoft.com/library/mt238486.aspx).

##  <a name="infotipimageshiproominfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Comunicación con el equipo de ingeniería de SQL Server 
- [Stack Overflow en español (etiqueta sql server): preguntas técnicas](http://stackoverflow.com/questions/tagged/sql-server)
- [Foros de MSDN: preguntas técnicas](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: informar sobre errores y solicitar características](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: debate general sobre R](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
