---
title: Almacén de administración de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], management data warehouse
- data warehouse
- management data warehouse
ms.assetid: 9874a8b2-7ccd-494a-944c-ad33b30b5499
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26f75c135fdc0dcbcc5534a019ff6658d7c9e88e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089315"
---
# <a name="management-data-warehouse"></a>almacén de administración de datos
  El almacén de administración de datos es una base de datos relacional que contiene los datos recopilados de un servidor que es el destino de la recopilación de datos. Estos datos se utilizan para generar informes para los conjuntos de recopilación de datos del sistema y también pueden utilizarse para crear informes personalizados.  
  
 La infraestructura del recopilador de datos define los trabajos y los planes de mantenimiento que se necesitan para implementar las directivas de retención definidas por el administrador de bases de datos.  
  
> [!IMPORTANT]  
>  Para esta versión del recopilador de datos, el almacén de datos de administración se crea utilizando el modelo de recuperación simple, para minimizar el registro. Debe implementar el modelo de recuperación adecuado para su organización.  
  
## <a name="deploying-and-using-the-data-warehouse"></a>Implementar y usar el almacenamiento de datos  
 Puede instalar el almacén de administración de datos en la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecuta el recopilador de datos. Sin embargo, si los recursos o el rendimiento del servidor suponen un problema en el servidor que se está supervisando, puede instalar el almacén de administración de datos en otro equipo.  
  
 Al crear el almacén de administración de datos, se crean los esquemas necesarios y sus objetos para los conjuntos de recopilación del sistema predefinidos. Se crean dos esquemas, el de núcleo y el de instantáneas. Se crea un tercer esquema, custom_snapshots, cuando se crean conjuntos de recopilación definidos por el usuario que incluyen elementos de recopilación que usan el tipo de recopilador de consultas T-SQL genérico.  
  
###### <a name="core-schema"></a>Esquema de núcleo  
 El esquema de núcleo define las tablas, los procedimientos almacenados y las vistas que se usan para organizar e identificar los datos recopilados. Estas tablas se comparten entre todas las tablas de datos creadas para los tipos de recopilador individuales. Este esquema está bloqueado y solamente lo puede modificar el propietario de la base de datos del almacén de administración de datos. Los nombres de las tablas de este esquema llevan el prefijo "core".  
  
 En la tabla siguiente se describen las tablas de base de datos del esquema de núcleo. Estas tablas de base de datos permiten al recopilador de datos realizar el seguimiento de la procedencia de los datos y saber quién los insertó y cuándo se cargaron en el almacenamiento de datos.  
  
|Nombre de la tabla|Descripción|  
|----------------|-----------------|  
|core.performance_counter_report_group_items|Almacena información sobre la forma en que se deben agrupar y agregar los contadores de rendimiento en los informes del almacén de administración de datos.|  
|core.snapshots_internal|Identifica cada nueva instantánea. En esta tabla se inserta una nueva fila cada vez que un paquete de carga inicia la carga de un nuevo lote de datos.|  
|core.snapshot_timetable_internal|Almacena información sobre la hora de la instantánea. La hora de la instantánea se almacena en una tabla independiente, porque pueden producirse muchas instantáneas prácticamente a la vez.|  
|core.source.info_internal|Esta tabla almacena información sobre el origen de datos. Se actualiza esta tabla cuando un nuevo conjunto de recopilación empieza a cargar los datos en el almacén de datos.|  
|core.supported_collector_types_internal|Contiene los identificadores de los tipos de recopilador registrados que pueden cargar datos en el almacén de administración de datos. Esta tabla solo se actualiza cuando el esquema del almacén de datos se actualiza para admitir un nuevo tipo de recopilador. Cuando se crea el almacén de administración de datos, esta tabla se rellena con los identificadores de los tipos de recopilador proporcionados por el recopilador de datos.|  
|core.wait_categories|Contiene las categorías utilizadas para agrupar los tipos de espera de acuerdo con la característica wait_type.|  
|core.wait_types|Contiene los tipos de espera reconocidos por el recopilador de datos.|  
|core.purge_info_internal|Indica que se ha realizado una solicitud para detener la eliminación de datos en el almacén de administración de datos.|  
  
 Las tablas anteriores se utilizan con tablas de tipo de recopilador para almacenar información. Por ejemplo, el tipo de recopilador genérico de Seguimiento de SQL usa las tablas siguientes para almacenar los datos de seguimiento:  
  
-   core.source_info_internal  
  
-   core.snapshots_internal  
  
-   snapshots.trace_info  
  
-   snapshots.trace_data  
  
###### <a name="snapshots-schema"></a>Esquema de instantáneas  
 El esquema de instantáneas describe los objetos necesarios para almacenar y mantener los datos recopilados por los tipos de recopilador que se proporcionan. Las tablas de este esquema son fijas y no necesitan cambiarse durante la vigencia del tipo de recopilador. Si se necesitan cambios, solo los miembros del rol mdw_admin pueden cambiar el esquema. Estas tablas se crean para almacenar los datos recopilados por los conjuntos de recopilación de datos del sistema.  
  
 En las tablas siguientes se muestra una parte del esquema del almacén de administración de datos que se requiere para los conjuntos de recopilación de actividad del servidor y de estadísticas de consultas.  
  
-   Tablas de recursos de nivel del sistema  
  
    -   **snapshots.os_wait_stats**  
  
    -   **snapshots.os_latch_stats**  
  
    -   **snapshots.os_schedulers**  
  
    -   `snapshots.os_memory_clerks`  
  
    -   **snapshots.os_memory_nodes**  
  
    -   snapshots.sql_process_and_system_memory  
  
-   Actividad del sistema  
  
    -   snapshots.active_sessions_and_requests  
  
-   Estadísticas de consultas  
  
    -   snapshots.query_stats  
  
-   Estadísticas de E/S  
  
    -   `snapshots.io_virtual_file_stats`  
  
-   Texto y plan de consulta  
  
    -   snapshots.notable_query_text  
  
    -   snapshots.notable_query_plan  
  
-   Estadísticas de consultas normalizadas  
  
    -   snapshots.distinct_queries  
  
    -   snapshots.distinct_query_to_handle  
  
 **Esquema custom_snapshots**  
  
 El esquema custom_snapshots describe las tablas y las vistas nuevas que se crean cuando se utilizan tipos de recopilador estándar o de otros fabricantes para crear los conjuntos de recopilación definidos por el usuario. Cualquier tipo de recopilador que requiera una nueva tabla de datos para un elemento de recopilación puede crear esa tabla en este esquema. Los miembros del rol mdw_writer pueden agregar nuevas tablas a este esquema. Cualquier otro cambio en el esquema solo lo pueden realizar los miembros del rol mdw_admin.  
  
 Para obtener información detallada sobre el tipo de datos y el contenido de las columnas de tabla de base de datos, lea la documentación del procedimiento almacenado del recopilador de datos correspondiente de cada una de las tablas.  
  
### <a name="best-practices"></a>Procedimientos recomendados  
 Al trabajar con el almacén de datos de administración, recomendamos seguir estas prácticas recomendadas:  
  
-   No modifique los metadatos de tablas de almacén de datos de administración a menos que esté agregando un nuevo tipo de recopilador.  
  
-   No modifique directamente los datos del almacén de datos de administración. Al cambiar los datos que ha recopilado, se invalida la legitimidad de los datos recopilados.  
  
-   En lugar de usar las tablas directamente, use los procedimientos almacenados y las funciones que se proporcionan con el recopilador de datos para obtener acceso a los datos de instancia y aplicación. Los nombres y las definiciones de las tablas se pueden cambiar, cambian al actualizar la aplicación y pueden cambiar en versiones futuras.  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se ha agregado la tabla core.performance_counter_report_group_items a la sección "Esquema de núcleo".|  
|Se ha actualizado la lista de tablas de la sección "Esquema de instantáneas". Se ha agregado snapshots.os_memory_clerks, snapshots.sql_process_and_system_memory y snapshots.io_virtual_file_stats. Se ha quitado snapshots.os_process_memory y snapshots.distinct_query_stats.|  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de almacén de administración de datos &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql)   
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)   
 [Recopilación de datos](data-collection.md)   
 [Ver un informe de conjunto de recopilación &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
  
