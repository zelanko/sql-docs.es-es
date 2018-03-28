---
title: Notas de la versión de SQL Server 2016 | Microsoft Docs
ms.date: 03/14/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
caps.latest.revision: ''
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1a6d422098fdacb3a7bc6392b99fe63bb25c2c36
ms.sourcegitcommit: 6e16d1616985d65484c72f5e0f34fb2973f828f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2018
---
# <a name="sql-server-2016-release-notes"></a>Notas de la versión de SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  En este artículo se describen las limitaciones y los problemas de las versiones de SQL Server 2016, incluidos los Service Packs. Para obtener más información sobre las novedades, vea el artículo de [novedades de SQL Server 2016](https://docs.microsoft.com/en-us/sql/sql-server/what-s-new-in-sql-server-2016).

> [![Descargar desde el Centro de evaluación](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)  Descargar SQL Server 2016 desde el **[Centro de evaluación](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**
>
> [![Azure Virtual Machine pequeña](../includes/media/azure-vm.png)](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/) ¿Tiene una cuenta de Azure?  Si es así, vaya **[aquí](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** para poner en marcha una máquina virtual con SQL Server 2016 SP1 ya instalado.
>
> [![Descargar SSMS](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) Para obtener la versión más reciente de SQL Server Management Studio, vea **[Descarga de SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)**.

## <a name="bkmk_2016sp1"></a>SQL Server 2016 Service Pack 1 (SP1)
![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP1 incluye todas las revisiones hasta SQL Server 2016 RTM CU3, incluida la actualización de seguridad MS16-136. Contiene una acumulación de soluciones proporcionadas en las actualizaciones acumulativas de SQL Server 2016 e incluye la actualización acumulativa más reciente (CU3) y la actualización de seguridad MS16-136, publicada el 8 de noviembre de 2016. 

Están disponibles las siguientes características en las ediciones Standard, Web, Express y Base de datos local de SQL Server SP1 (salvo que se indique lo contrario):
- Always Encrypted
- Captura de datos modificada (no disponible en Express)
- columnstore
- Compresión
- Enmascaramiento de datos dinámicos
- Auditoría específica
- OLTP en memoria (no disponible en Base de datos local)
- Varios contenedores de secuencias de archivos (no disponibles en Base de datos local)
- Particiones
- Polybase
- Seguridad de nivel de fila

En la siguiente tabla se resumen las mejoras principales proporcionadas en SQL Server 2016 SP1.

|Característica|Description|Para obtener más información|
|---|---|---|
|Inserción masiva en montones con TABLOCK automático en TF 715| La marca de seguimiento 715 permite el bloqueo de tabla para operaciones de carga masiva en un montón sin índices no agrupados.|[Migrating SAP workloads to SQL Server just got 2.5x faster](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/) (La migración de las cargas de trabajo de SAP a SQL Server ahora es 2,5 veces más rápida)|
|CREATE OR ALTER|Implementación de objetos (por ejemplo, procedimientos almacenados, desencadenadores, funciones definidas por el usuario o vistas).|[Blog del Motor de base de datos de SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/11/17/create-or-alter-another-great-language-enhancement-in-sql-server-2016-sp1/)|
|Compatibilidad con DROP TABLE para la replicación|Compatibilidad con DROP TABLE DDL para la replicación para que se puedan quitar artículos de replicación.|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)|
|Firma del controlador FileStream RsFx|El controlador Filestream RsFx se firma y se certifica mediante el portal del panel del centro de desarrolladores de hardware de Windows (portal de desarrollo), que permite instalar el controlador Filestream RsFx de SQL Server 2016 SP1 en Windows Server 2016 o en Windows 10 sin ningún problema.|[Migrating SAP workloads to SQL Server just got 2.5x faster](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/) (La migración de las cargas de trabajo de SAP a SQL Server ahora es 2,5 veces más rápida)|
|LPIM en una cuenta de servicio SQL: identificación mediante programación|Permite a los DBA identificar mediante programación si el privilegio Bloquear páginas en la memoria (LPIM) está en vigor en el momento de iniciar el servicio.|[Elección de los desarrolladores: identificar mediante programación privilegios LPIM e IFI en SQL Server](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-programmatically-identify-lpim-and-ifi-privileges-in-sql-server)|
|Limpieza de seguimiento de cambios manual|El nuevo procedimiento almacenado limpia la tabla interna de seguimiento de cambios a petición.| [KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)|
|Cambios del operador INSERT..SELECT paralelo en las tablas temporales locales|Nuevo operador INSERT paralelo en operaciones INSERT..SELECT.|[Equipo de asesoramiento al cliente de SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/07/21/real-world-parallel-insert-what-else-you-need-to-know/)|
|Showplan XML|Se ha ampliado el diagnóstico, que incluye la advertencia de concesiones y la memoria máxima habilitada para una consulta, marcas de seguimiento habilitadas y la exposición de otros datos de diagnóstico. | [KB 3190761](https://support.microsoft.com/help/3190761/update-to-improve-diagnostics-by-expose-data-type-of-the-parameters-fo)|
|Memoria de la clase de almacenamiento|Mejore el procesamiento de transacciones usando la memoria de la clase de almacenamiento en Windows Server 2016, lo que permite acelerar los tiempos de confirmación de transacciones por órdenes de la magnitud.|[Blog del Motor de base de datos de SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)|
|USE HINT|Use la opción de consulta `OPTION(USE HINT('<option>'))` para modificar el comportamiento del optimizador de consultas usando sugerencias de nivel de consulta admitidas. A diferencia de QUERYTRACEON, la opción USE HINT no requiere ningún privilegio de administrador del sistema.|[Elección de los desarrolladores: sugerencias de consulta USE HINT](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-use-hint-query-hints/)|
|Adiciones de XEvent|Las nuevas capacidades de diagnóstico de rendimiento y de XEvents mejoran la resolución de problemas de latencia.|[Eventos extendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)|

Además, tenga en cuenta las revisiones siguientes:
- A partir de los comentarios de los DBA y de la comunidad de SQL, a partir de SQL 2016 SP1, lo mensajes de registro de Hekaton se han reducido al mínimo.
- Revise las nuevas [marcas de seguimiento](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).
- Las versiones completas de las bases de datos de ejemplo de WideWorldImporters ya funcionan con las ediciones Standard y Express a partir de SQL Server 2016 SP1 y están disponibles en [Github]( https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0). En el ejemplo no es necesario efectuar ningún cambio. Las copias de seguridad de base de datos creadas en RTM para la edición Enterprise funcionan con las ediciones Standard y Express en SP1. 

La instalación de SQL Server 2016 SP1 puede requerir el reinicio después de la instalación. Como procedimiento recomendado, se aconseja planear y llevar a cabo un reinicio después de la instalación de SQL Server 2016 SP1.

### <a name="download-pages-and-more-information"></a>Páginas de descarga y más información

- [Descargar Service Pack 1 para Microsoft SQL Server 2016](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 Service Pack 1 (SP1) publicado](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)
- [Información de lanzamiento de SQL Server 2016 Service Pack 1](https://support.microsoft.com/kb/3182545)
- ![info_tip](../sql-server/media/info-tip.png) [Centro de actualización de SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) para obtener vínculos e información de todas las versiones compatibles, incluidos los Service Packs de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 

##  <a name="bkmk_2016_ga"></a>SQL Server 2016 Release: Disponibilidad general
-   [Motor de base de datos (disponibilidad general)](#bkmk_ga_instalpatch) 
-   [Stretch Database (disponibilidad general)](#bkmk_ga_stretch)
-   [Almacén de consultas (disponibilidad general)](#bkmk_ga_query_store)
-   [Documentación del producto (disponibilidad general)](#bkmk_ga_docs)
 
### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> Install Patch Requirement (GA) 
**Problema e impacto en el cliente:** Microsoft ha identificado un problema con los archivos binarios en tiempo de ejecución de Microsoft VC++ 2013, que se instalan como requisito previo de SQL Server 2016. Hay disponible una actualización para corregir este problema. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server 2016 experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server 2016, compruebe si el equipo necesita la revisión descrita en [KB 3164398](http://support.microsoft.com/kb/3164398). La revisión también está incluida en el [paquete de actualizaciones acumulativas 1 (CU1) para SQL Server 2016 RTM](https://www.microsoft.com/download/details.aspx?id=53338). 

**Solución:** use una de las siguientes soluciones:

- Instale [la actualización de Visual C++ 2013 y del paquete redistribuible de Visual C++ (KB 3138367)](http://support.microsoft.com/kb/3138367). KB es el método preferido. Puede instalarla antes o después de instalar SQL Server 2016. 

    Si SQL Server 2016 ya está instalado, haga lo siguiente en este orden:

    1.  Descargue el archivo *vcredist_\*exe* que proceda.
    1.  Detenga el servicio SQL Server de todas las instancias del motor de base de datos.
    1.  Instale **KB 3138367**.
    1.  Reinicie el equipo.
 

 - Instale la  [actualización crítica para requisitos previos de MSVCRT de SQL Server 2016 (KB 3164398)](http://support.microsoft.com/kb/3164398).  
 
    Si se decanta por **KB 3164398**, puede instalar durante la instalación de SQL Server, a través de Microsoft Update o desde el Centro de descarga de Microsoft. 

    - **Durante la instalación de SQL Server 2016:** si el equipo donde se ejecuta el programa de instalación de SQL Server tiene acceso a Internet, el programa de instalación de SQL Server busca la actualización como parte de la instalación global de SQL Server. Si acepta la actualización, el programa de instalación descarga y actualiza los archivos binarios durante la instalación.

    - **Microsoft Update:** la actualización está disponible en Microsoft Update como una actualización crítica de SQL Server 2016 no de seguridad. Si la instalación se realiza a través de Microsoft Update (esto es, después de SQL Server 2016), es necesario reiniciar el servidor después de actualizar. 

    - **Centro de descarga:** por último, la actualización también está disponible desde el Centro de descarga de Microsoft. Puede descargar el software correspondiente a la actualización e instalarlo en los servidores cuando tengan instalado SQL Server 2016. 


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>Problema con un carácter específico de un nombre de tabla o de base de datos

**Problema e impacto sobre el cliente:** al intentar habilitar Stretch Database en una base de datos o una tabla se produce un error. El problema se produce cuando el nombre del objeto incluye un carácter que se trata como otro distinto al convertir de minúsculas a mayúsculas. Un ejemplo de un carácter que provoca este problema es "ƒ" (combinación de teclas: ALT+159).

**Solución alternativa:** si quiere habilitar Stretch Database en la base de datos o en la tabla, la única opción consiste en cambiar el nombre del objeto y quitar el carácter problemático.

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>Problema con un índice en el que se usa la palabra clave INCLUDE

**Problema e impacto en el cliente:** se produce un error al intentar habilitar Stretch Database en una tabla que tiene un índice en el que se usa la palabra clave INCLUDE para incluir más columnas.

**Solución alternativa:** quite el índice en el que se usa la palabra clave INCLUDE, habilite Stretch Database en la tabla y, luego, vuelva a crear el índice. Si lo hace, procure respetar las prácticas y directivas de mantenimiento de su organización para evitar o minimizar cualquier impacto en los usuarios de la tabla afectada.

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Problema con la limpieza automática de los datos en las ediciones distintas de Enterprise y Developer

 **Problema e impacto en el cliente:** no se puede llevar a cabo una limpieza automática de los datos en las ediciones distintas de Enterprise y Developer. Por lo tanto, si los datos no se purgan de forma manual, el espacio usado por el Almacén de consultas crece con el tiempo hasta que se alcanza el límite configurado. Si no se soluciona, este problema también rellena el espacio en disco asignado a los registros de errores, ya que cada intento de ejecutar una limpieza crea un archivo de volcado. El período de activación de limpieza depende de la frecuencia de la carga de trabajo, pero no es superior a 15 minutos.

 **Solución alternativa:** si tiene previsto usar el almacén de consultas en ediciones distintas de Enterprise y Developer, tendrá que desactivar expresamente las directivas de limpieza. Esto se puede hacer desde SQL Server Management Studio (página Propiedades de la base de datos) o a través de este script de Transact-SQL:

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

Considere también las opciones de limpieza manual para impedir que el almacén de consultas pase a modo de solo lectura. Por ejemplo, ejecute la siguiente consulta para limpiar periódicamente el espacio de datos completo:

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

De igual modo, ejecute regularmente los siguientes procedimientos almacenados de almacén de consultas para limpiar las estadísticas de tiempo de ejecución o consultas o planes específicos:

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> Documentación del producto (disponibilidad general) 
 **Problema e impacto en el cliente:** aún no está disponible una versión descargable de la documentación de SQL Server 2016. Cuando use el Administrador de bibliotecas de ayuda para intentar **instalar contenido desde Internet**, verá la documentación de SQL Server 2012 y SQL Server 2014, pero ninguna opción para la documentación de SQL Server 2016.    
    
 **Solución alternativa:** use una de las siguientes soluciones:    
    
 ![Administrar la configuración de la Ayuda de SQL Server](../sql-server/media/docs-sql2016-managehelpsettings.png "Administrar la configuración de la Ayuda de SQL Server")    
    
-   **Elegir Ayuda en línea o local** para configurar la ayuda para "Quiero usar la Ayuda en línea".    
    
-   **Instalar contenido desde Internet** y descargar el contenido de SQL Server 2014.    
    
 **F1 Ayuda:** por diseño, cuando se pulsa F1 en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], la versión en línea del artículo de F1 Ayuda se muestra en el explorador. El problema es que aparece la ayuda basada en el explorador incluso si se ha configurado e instalado la ayuda local. 
     
**Actualización de contenido:**    
En SQL Server Management Studio y Visual Studio, la aplicación del Visor de Ayuda puede bloquearse mientras se agrega la documentación. Para solucionar este problema, realice los siguientes pasos. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](https://msdn.microsoft.com/library/mt654096.aspx)(El Visor de Ayuda de Visual Studio se bloquea).    
    
* Abra el archivo %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings en el Bloc de notas y cambie la fecha en el siguiente código a una fecha en el futuro.    
    
     
```    
     Cache LastRefreshed="12/31/2017 00:00:00"    
``` 

## <a name="additional-information"></a>Información adicional
+ [Instalación de SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [Vínculos e información del Centro de actualizaciones de SQL Server sobre todas las versiones compatibles](https://msdn.microsoft.com/library/ff803383.aspx)


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]    

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")    
