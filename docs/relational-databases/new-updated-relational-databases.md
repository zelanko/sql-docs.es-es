---
title: 'Actualizados: documentos de bases de datos relacionales | Microsoft Docs'
description: "Muestra fragmentos del contenido actualizado en la documentación de bases de datos relacionales que ha cambiado recientemente."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 1fbc7affa833eb34b6e13e28b229d47ac0b05a5c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Nuevos y actualizados recientemente: documentos de bases de datos relacionales



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área temática:* &nbsp; **Bases de datos relacionales**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Use the SSMS XEvent Profiler (Uso del generador de perfiles XEvent de SSMS)](extended-events/use-the-ssms-xe-profiler.md)
2. [Importación de archivos planos mediante el asistente de SQL](import-export/import-flat-file-wizard.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Base de datos tempdb](#TitleNum_1)
2. [Guía de arquitectura de administración de memoria](#TitleNum_2)
3. [Estadísticas](#TitleNum_3)
4. [sp_server_diagnostics (Transact-SQL)](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>1. &nbsp; [Base de datos tempdb](databases/tempdb-database.md)

*Actualizado: 20-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 121.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c8bb5f9c40625aaf955295e5b5d03e4257e6c6b 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d  (PR=4039  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=ef1fa818beea435f58986af3379853dc28f5efd8) -->



**Optimización del rendimiento de tempdb**

 El tamaño y la ubicación física de la base de datos tempdb puede afectar al rendimiento de un sistema. Por ejemplo, si el tamaño definido en tempdb es demasiado pequeño, parte de la carga de procesamiento del sistema puede deberse al crecimiento automático de tempdb hasta el tamaño necesario para admitir la carga de trabajo cada vez que se reinicia la instancia de ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)].

 Si es posible, use la [inicialización instantánea de archivos de base de datos--../../relational-databases/databases/database-instant-file-initialization.md) para mejorar el rendimiento de las operaciones de crecimiento de archivos de datos.

 Asigne espacio previamente para todos los archivos de tempdb estableciendo el tamaño de archivo en un valor lo suficientemente alto para acomodar la carga de trabajo habitual del entorno. Así se evita que tempdb se expanda con demasiada frecuencia, lo que puede afectar al rendimiento. La base de datos tempdb debe establecerse de modo que crezca automáticamente, pero solo con el fin de aumentar el espacio en disco para las excepciones no previstas.

 Los archivos de datos deben ser del mismo tamaño dentro de cada [grupo de archivos-../../relational-databases/databases/database-files-and-filegroups.md#filegroups), dado que ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] usa un algoritmo de relleno proporcional que favorece las asignaciones en los archivos con más espacio libre. La división de tempdb en varios archivos de datos del mismo tamaño proporciona un alto grado de eficiencia paralela en las operaciones que usan tempdb.

 Establezca el incremento de crecimiento de archivos en un tamaño razonable para evitar que los archivos de la base de datos tempdb crezcan en un porcentaje demasiado pequeño. Si el crecimiento de los archivos es demasiado pequeño comparado con la cantidad de datos que se escriben en tempdb, es posible que sea necesario expandir tempdb constantemente. Esto afectará al rendimiento.

 Para comprobar los parámetros actuales de tamaño y de crecimiento de tempdb, use la consulta siguiente:
```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeinMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-memory-management-architecture-guidememory-management-architecture-guidemd"></a>2. &nbsp; [Guía de arquitectura de administración de memoria](memory-management-architecture-guide.md)

*Actualizado: 28-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Siguiente](#TitleNum_3))

<!-- Source markdown line 75.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 dd47431ca47eab16af40e41adaeeaf3fc5fb7461 445f013af3bdad65dd3eaf837db7f744b43e8f97  (PR=4113  ,  Filename=memory-management-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



En versiones anteriores de SQL Server (..!NCLUDE-NotShown--ssVersion2005--../includes/ssversion2005-md.md)], ..!NCLUDE-NotShown--ssKatmai--../includes/ssKatmai-md.md)] y ..!NCLUDE-NotShown--ssKilimanjaro--../includes/ssKilimanjaro-md.md)]), la asignación de memoria se realizaba con cinco mecanismos diferentes:
-  **Asignador de una página (SPA)**, incluidas solo las asignaciones de memoria menores o iguales a 8 KB en el proceso de ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)]. Las opciones de configuración *memoria de servidor máxima (MB)* y *memoria de servidor mínima (MB)* determinaban los límites de la memoria física que podía consumir el SPA. El grupo de búferes era el mecanismo para SPA y el mayor consumidor de asignaciones de página única.
-  **Asignador de varias páginas (MPA)**, para las asignaciones de memoria que solicitan más de 8 KB.
-  **Asignador de CLR**, que incluye las pilas CLR de SQL y las asignaciones globales creadas durante la inicialización de CLR.
-  Las asignaciones de memoria para **[pilas de subprocesos--../relational-databases/memory-management-architecture-guide.md#stacksizes)** en el proceso de ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)].
-  **Asignaciones de Windows directas**, para las solicitudes de asignación de memoria que se hacen directamente a Windows. Estas incluyen el uso del montón de Windows y las asignaciones virtuales directas realizadas por los módulos que se cargan en el proceso de ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)]. Algunos ejemplos de estas solicitudes de asignaciones de memoria incluyen asignaciones de DLL de procedimiento almacenado extendido, objetos que se crean mediante procedimientos de Automation (llamadas sp_OA) y asignaciones para proveedores de servidores vinculados.

A partir de ..!NCLUDE-NotShown--ssSQL11--../includes/sssql11-md.md)], las asignaciones de una página, de varias páginas y de CLR están consolidadas en un **Asignador de páginas de "cualquier tamaño"**, y se incluye en los límites de memoria controlados por las opciones de configuración *memoria de servidor máxima (MB)* y *memoria de servidor mínima (MB)*. Este cambio proporcionó una capacidad de ajuste de tamaño más precisa para todos los requisitos de memoria que pasan por el administrador de memoria de ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)].



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-statisticsstatisticsstatisticsmd"></a>3. &nbsp; [Estadísticas](statistics/statistics.md)

*Actualizado: 27-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2) | [Siguiente](#TitleNum_4))

<!-- Source markdown line 48.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1dbe3bd6fdfcd27cf4a597cac5a4a09821b51ba7 971cfccf75fbc8842a0ef020a2bc93992c5f4ad9  (PR=4087  ,  Filename=statistics.md  ,  Dirpath=docs\relational-databases\statistics\  ,  MergeCommitSha40=9fbe5403e902eb996bab0b1285cdade281c1cb16) -->



> [!NOTE]
> Los histogramas de ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] solo se generan para una única columna (la primera del conjunto de columnas de clave del objeto de estadísticas).

Para crear el histograma, el optimizador de consultas ordena los valores de columna, calcula el número de valores que coinciden con cada valor de columna distinto y, a continuación, agrupa los valores de columna en un máximo de 200 pasos de histograma contiguos. Cada paso del histograma incluye un intervalo de valores de columna seguido de un valor de columna de límite superior. El intervalo incluye todos los valores de columna posibles comprendidos entre los valores límite (sin incluir los propios valores límite). El valor de columna ordenado más pequeño es el valor del límite superior del primer paso del histograma.

Con más detalle, ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] crea el **histograma** a partir del conjunto ordenado de valores de columna en tres pasos:

- **Inicialización del histograma**: en el primer paso, se procesa una secuencia de valores desde el principio del conjunto ordenado y se recopila un máximo de 200 valores de *range_high_key*, *equal_rows*, *range_rows* y *distinct_range_rows* (*range_rows* y *distinct_range_rows* son siempre cero durante este paso). El primer paso finaliza cuando se han agotado todas las entradas o cuando se han encontrado 200 valores.
- **Examen con combinación de depósito**: cada valor adicional de la columna inicial de la clave de estadísticas se procesa en el segundo paso, de forma ordenada; cada valor sucesivo se agrega al último intervalo o se crea un intervalo nuevo al final (esto es posible porque los valores de entrada están ordenados). Si se crea un intervalo nuevo, un par de intervalos existentes colindantes se contrae en un solo intervalo. Este par de intervalos se selecciona para minimizar la pérdida de información. Este método usa un algoritmo de *diferencias máximas* para minimizar el número de pasos del histograma a la vez que maximiza las diferencias entre los valores de límite. El número de pasos después de contraer los rangos permanece en 200 a lo largo de este paso.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-spserverdiagnostics-transact-sqlsystem-stored-proceduressp-server-diagnostics-transact-sqlmd"></a>4. &nbsp; [sp_server_diagnostics (Transact-SQL)](system-stored-procedures/sp-server-diagnostics-transact-sql.md)

*Actualización: 21-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3))

<!-- Source markdown line 157.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d0d97efbb0b16638d0120af9ac5e66ec3bcfa391 b98735ec26a091f8c8c58ca1790243be7942e038  (PR=4052  ,  Filename=sp-server-diagnostics-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=45e4efb7aa828578fe9eb7743a1a3526da719555) -->



En la consulta de ejemplo siguiente se lee la salida de resumen de la tabla:
```sql
SELECT create_time,
       component_name,
       state_desc
FROM SpServerDiagnosticsResult;
```

En la consulta de ejemplo siguiente se leen parte de los resultados detallados de cada componente de la tabla:
```sql
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult
where component_name like 'resource'
go

-- Nonpreemptive waits
```







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos + Actualizados (3+14): documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + Actualizados (1+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (87+0): documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + Actualizados (5+4): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + Actualizados (0+1): documentos de **Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + Actualizados (2+2): documentos de **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + Actualizados (10+9): documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + Actualizados (2+4): documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + Actualizados (4+2): documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + Actualizados (0+1): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (21+0): documentos de **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + Actualizados (5+1): documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + Actualizados (1+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + Actualizados (0+2): documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


