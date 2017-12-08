---
title: "Administración y supervisión de la búsqueda de texto completo para una instancia de servidor | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], about
- full-text search [SQL Server], server management
ms.assetid: 2733ed78-6d33-4bf9-94da-60c3141b87c8
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5d37441c773b2934b544734889a9d7c86cbdfa2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="manage-and-monitor-full-text-search-for-a-server-instance"></a>Administrar y supervisar la búsqueda de texto completo para una instancia de servidor
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] La administración de texto completo de una instancia del servidor incluye:  
  
-   Tareas de administración del sistema como administrar el servicio del iniciador de FDHOST (MSSQLFDLauncher), reiniciar el proceso de host de demonio de filtro si cambia las credenciales de la cuenta de servicio, configurar las propiedades de texto completo del servidor y realizar copia de seguridad de los catálogos de texto completo. En el nivel del servidor, por ejemplo, puede especificar un idioma de texto completo predeterminado que sea diferente del idioma predeterminado de la instancia del servidor en su totalidad.  
  
-   Configurar componentes lingüísticos de texto completo (separadores de palabras y lematizadores, archivo de diccionario de sinónimos y palabras irrelevantes y listas de palabras irrelevantes).  
  
-   Configurar una base de datos de usuario para la búsqueda de texto completo. Esto implica crear uno o más catálogos de texto completo para la base de datos y definir un índice de texto completo en cada tabla o vista indizada en la que desee ejecutar las consultas de texto completo.  
  
##  <a name="props"></a> Ver o cambiar las propiedades del servidor para la búsqueda de texto completo  
 Puede ver las propiedades de texto completo de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-view-and-change-server-properties-for-full-text-search"></a>Para ver y cambiar las propiedades del servidor para la búsqueda de texto completo  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y luego haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades del servidor** , haga clic en la página **Avanzadas** para ver información del servidor sobre la búsqueda de texto completo. Las propiedades de texto completo son las siguientes:  
  
    -   **Idioma de texto completo predeterminado**  
  
         Especifica un idioma predeterminado para las columnas indizadas de texto completo. El análisis lingüístico de los datos de texto completo indizados depende del idioma de los datos. El valor predeterminado de esta opción es el idioma del servidor. Para saber qué idioma corresponde al valor mostrado, vea [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
    -   **Opción de actualización de catálogo de texto completo**  
  
         Esta propiedad de servidor controla cómo se migran los índices de texto completo cuando se actualiza una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a una versión posterior. Esta propiedad se aplica a la actualización al adjuntar una base de datos, restaurar una copia de seguridad de base de datos, restaurar una copia de seguridad de archivo o copiar la base de datos mediante el Asistente para copiar bases de datos.  
  
         Las alternativas son las siguientes:  
  
         **Importar**  
         Se importan los catálogos de texto completo. Normalmente, el proceso de importación es significativamente más rápido que el de regeneración. Por ejemplo, si se usa solo una CPU, importar es aproximadamente 10 veces más rápido que volver a generar. Sin embargo, un catálogo de texto completo importado no usa los separadores de palabras nuevos y mejorados de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], por lo que es posible que, al final, le interese volver a generar los catálogos de texto completo.  
  
        > [!NOTE]  
        >  La recompilación se puede ejecutar en modo de varios subprocesos; además, si hay más de 10 CPU disponibles y permite que el proceso de recompilación las use todas, dicho proceso puede resultar más rápido que el de importación.  
  
         Si un catálogo de texto completo no está disponible, se vuelven a generar los índices de texto completo asociados. Esta opción solo está disponible para bases de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
         **Volver a generar**  
         Los catálogos de texto completo se vuelven a generar con los separadores de palabras nuevos y mejorados. La regeneración de los índices puede llevar cierto tiempo y, después de la actualización, podría ser necesaria una cantidad significativa de CPU y de memoria.  
  
         **Restablecer**  
         Los catálogos de texto completo se restablecen. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Los archivos de catálogo de texto completo se quitan, pero los metadatos de los catálogos de texto completo y los índices de texto completo se conservan. Después de actualizarse, todos los índices de texto completo quedan deshabilitados para el seguimiento de cambios y los rastreos no se inician de forma automática. El catálogo permanecerá vacío hasta que se emita manualmente un rellenado completo después de que se complete la actualización.  
  
         Para obtener información sobre cómo elegir una opción de actualización de texto completo, vea[Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
        > [!NOTE]  
        >  La opción de actualización de texto completo también se puede establecer mediante la acción [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)**upgrade_option** .  
  
##  <a name="metadata"></a> Ver propiedades de servidor de texto completo adicionales  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] Las funciones se pueden usar para obtener el valor de varias propiedades de búsqueda de texto completo de nivel de servidor. Esta información es útil para administrar y solucionar problemas de la búsqueda de texto completo.  
  
 En la tabla siguiente se enumeran las propiedades de texto completo de una instancia de servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus funciones [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionadas.  
  
|Propiedad|Descripción|Función|  
|--------------|-----------------|--------------|  
|**IsFullTextInstalled**|Si el componente de texto completo se instala con la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[FULLTEXTSERVICEPROPERTY](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)<br /><br /> [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)|  
||||  
|**LoadOSResources**|Si los separadores de palabras y filtros del sistema operativo se registran y utilizan con esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|FULLTEXTSERVICEPROPERTY|  
|**VerifySignature**|Especifica si el motor de texto completo carga únicamente datos binarios firmados.|FULLTEXTSERVICEPROPERTY|  
  
##  <a name="monitor"></a> Supervisar la actividad de búsqueda de texto completo  
 Para supervisar la actividad de búsqueda de texto completo en una instancia del servidor se pueden usar varias vistas y funciones de administración dinámica.  
  
 **Para ver información sobre los catálogos de texto completo con actividad de rellenado en curso**  
  
-   [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
  
 **Para ver la actividad actual de un proceso de host de demonio de filtro**  
  
-   [sys.dm_fts_fdhosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
  
 **Para ver información sobre la actividad de rellenado de índices en curso**  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
 **Para ver los búferes de un bloque de memoria utilizados como parte de un rastreo o intervalo de rastreo.**  
  
-   [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
  
 **Para ver los bloques de memoria compartida disponibles para el recopilador de texto completo en un rastreo de texto completo o un intervalo de rastreo de texto completo**  
  
-   [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
 **Para ver información acerca de cada lote de indización de texto completo**  
  
-   [sys.dm_fts_outstanding_batches &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
  
 **Para ver información sobre los intervalos específicos relacionados con una actividad de rellenado en curso**  
  
-   [sys.dm_fts_population_ranges &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
  
  
