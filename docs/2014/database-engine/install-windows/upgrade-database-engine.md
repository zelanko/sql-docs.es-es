---
title: Actualizar el motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4767b695f0c2c3668278e30f47f389664b4a4ef0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189555"
---
# <a name="upgrade-database-engine"></a>Actualizar el motor de base de datos
  Este tema proporciona información que necesitará para preparar y comprender el proceso de actualización; incluye:  
  
-   Problemas conocidos de actualización.  
  
-   Tareas y consideraciones previas a la actualización.  
  
-   Vínculos a temas de procedimientos para actualizar [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Vínculos a temas de procedimientos para migrar bases de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Consideraciones para clústeres de conmutación por error.  
  
-   Tareas y consideraciones posteriores a la actualización.  
  
## <a name="known-upgrade-issues"></a>Problemas conocidos de actualización  
 Antes de actualizar el [!INCLUDE[ssDE](../../includes/ssde-md.md)], revise [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../sql-server-database-engine-backward-compatibility.md). Para más información sobre escenarios de actualización admitidos y problemas conocidos de actualización, vea [Actualizaciones de ediciones y versiones admitidas](supported-version-and-edition-upgrades.md). Para obtener información sobre compatibilidad con versiones anteriores de otros componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Compatibilidad con versiones anteriores](../../getting-started/backward-compatibility.md).  
  
> [!IMPORTANT]  
>  Antes de actualizar de una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra, compruebe que las funciones que actualmente utiliza son compatibles con la edición a la que desea actualizar.  
  
> [!NOTE]  
>  Al actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] desde una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition, elija entre “Enterprise Edition: Licencia Core” y “Enterprise Edition”. Estas ediciones Enterprise solo se diferencian en los modos de licencia. Para obtener más información, consulte [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
## <a name="pre-upgrade-checklist"></a>Lista de comprobación previa a la actualización  
 El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la actualización a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde una versión anterior. También puede migrar las bases de datos de las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores. La migración puede ser de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra instancia del mismo equipo, o desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro equipo. Las opciones de migración incluyen el uso del Asistente para copiar bases de datos, la funcionalidad Copia de seguridad y restauración, el uso del Asistente para importar y exportar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los métodos de importación en bloque y exportación masiva.  
  
 Antes de actualizar el [!INCLUDE[ssDE](../../includes/ssde-md.md)], revise lo siguiente:  
  
-   Vea [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Vea [Check Parameters for the System Configuration Checker](check-parameters-for-the-system-configuration-checker.md).  
  
-   Vea [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
-   Revise [Actualizaciones de ediciones y versiones admitidas](supported-version-and-edition-upgrades.md).  
  
-   Revise [Usar el Asesor de actualizaciones para preparar las actualizaciones](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
-   Revise [Emplear Distributed Replay Utility para preparar las actualizaciones](../../sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md).  
  
-   Revise [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../sql-server-database-engine-backward-compatibility.md).  
  
-   Revise [Migrar los planes de consulta](change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
 Revise los problemas siguientes y realice los cambios antes de actualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Cuando actualice instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está dado de alta en relaciones de MSX/TSX, actualice los servidores de destino antes de actualizar los servidores maestros. Si actualiza los servidores maestros antes de actualizar los servidores de destino, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá conectarse a las instancias maestras de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Cuando actualice una edición de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una edición de 64 bits de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], deberá actualizar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] antes de actualizar el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Realice una copia de seguridad de todos los archivos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la instancia que va a actualizar, para que pueda restaurarlos al completo, si fuera necesario.  
  
-   Ejecute los comandos de consola de datos (DBCC) en las bases de datos que vaya a actualizar para asegurarse de que se encuentran en un estado coherente.  
  
-   Calcule el espacio en disco necesario para actualizar los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , así como las bases de datos de usuario. Para obtener el espacio en disco necesario para los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Requisitos de hardware y software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Asegúrese de que las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (maestra, de modelos, msdb y tempdb) existentes están configuradas para el crecimiento automático; asegúrese también de que tienen suficiente espacio disponible en disco duro.  
  
-   Asegúrese de que todos los servidores de bases de datos tienen información de inicio de sesión en la base de datos maestra. Esto es especialmente importante para restaurar las bases de datos, ya que la información de inicio de sesión del sistema reside en la base de datos maestra.  
  
-   Deshabilite todos los procedimientos almacenados de inicio, ya que el proceso de actualización se detendrá e iniciará los servicios en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se vaya a actualizar. Los procedimientos almacenados procesados al inicio podrían impedir el proceso de actualización.  
  
-   Asegúrese de que la replicación está vigente y, a continuación, detenga la replicación.  
  
-   Cierre todas las aplicaciones, incluidos los servicios que tengan dependencias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La actualización puede ser errónea si hay aplicaciones locales conectadas a la instancia que se va a actualizar.  
  
-   Si usa la creación de reflejo de la base de datos, vea [Minimizar el tiempo de inactividad de las bases de datos reflejadas al actualizar instancias de servidor](../database-mirroring/upgrading-mirrored-instances.md).  
  
## <a name="upgrading-the-database-engine"></a>Actualizar el Motor de base de datos  
 Puede sobrescribir una instalación de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior con una actualización de la versión. Si se detecta una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se actualizarán todos los archivos de programa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores y se conservarán todos los datos almacenados en la instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Además, las versiones anteriores de los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerán intactas en el equipo.  
  
> [!WARNING]  
>  Cuando se ejecuta el programa de instalación de SQL Server 2014, la instancia de SQL Server se detiene y reinicia como parte de la ejecución de las comprobaciones previas a la actualización.  
  
> [!CAUTION]  
>  Cuando actualice a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se sobrescribirá y ya no estará en el equipo. Antes de actualizar, realice una copia de seguridad de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de otros objetos asociados con la instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Puede actualizar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] con el Asistente para instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="database-compatibility-level-after-upgrade"></a>Nivel de compatibilidad de la base de datos después de la actualización  
 Los niveles de compatibilidad de la `tempdb`, `model`, `msdb` y **recursos** bases de datos se establecen en 120 después de la actualización. La base de datos del sistema `master` conserva el nivel de compatibilidad que tenía antes de la actualización.  
  
 Si el nivel de compatibilidad de una base de datos de usuario era 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad era 90 antes de la actualización, en la base de datos actualizada, el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Nuevas bases de datos de usuario heredarán el nivel de compatibilidad de la `model` base de datos.  
  
## <a name="migrating-databases"></a>Migrar bases de datos  
 Puede mover bases de datos de usuario a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando las funcionalidades de copias de seguridad y restauración o de adjuntar y separar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, vea [Copiar bases de datos con Copias de seguridad y restauración](../../relational-databases/databases/copy-databases-with-backup-and-restore.md) o [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
> [!IMPORTANT]  
>  Una base de datos que tenga el mismo nombre en los servidores de origen y de destino no se puede mover ni copiar. En este caso, aparecerá como "Ya existe".  
  
 Para obtener más información, vea [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="after-upgrading-the-database-engine"></a>Después de actualizar el Motor de base de datos  
 Después de actualizar el [!INCLUDE[ssDE](../../includes/ssde-md.md)], complete las siguientes tareas:  
  
-   Registre de nuevo los servidores. Para más información sobre cómo registrar los servidores, vea [Registrar servidores](../../ssms/register-servers/register-servers.md).  
  
-   Vuelva a rellenar los catálogos de texto completo para garantizar la coherencia semántica de los resultados de la consulta.  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instala nuevos separadores de palabras para ser usados en la búsqueda de texto completo y la búsqueda semántica. Los separadores de palabras se usan en el momento de la indización y en el momento de la consulta. Si no recompila los catálogos de texto completo, los resultados de la búsqueda pueden ser incoherentes. Si emite una consulta de texto completo que busca una frase que el separador de palabras de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] separó de forma diferente que el separador de palabras actual, es posible que no se recupere un documento o una fila que contengan la frase. Esto se debe a que las frases indizadas se separaron mediante una lógica diferente de la que está usando la consulta. La solución es volver a rellenar (volver a generar) los catálogos de texto completo con los nuevos separadores de palabras de modo que los comportamientos en el momento de la indización y en el momento de la consulta sean idénticos.  
  
     Para más información, vea [sp_fulltext_catalog &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql).  
  
-   Configure la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para reducir el área expuesta de un sistema susceptible de recibir ataques, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala y habilita de manera selectiva los servicios y características clave.  
  
-   Valide o quite las sugerencias de USE PLAN que genera [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y que se aplican a las consultas en las tablas con particiones e índices.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cambia la manera en que se procesan las consultas en tablas con particiones e índices. Las consultas en los objetos con particiones que usan la sugerencia USE PLAN para un plan generado por [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] podrían contener un plan que no se pueda usar en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Recomendamos que siga estos procedimientos después de actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
     **Cuando se especifica la sugerencia USE PLAN directamente en una consulta:**  
  
    1.  Quite la sugerencia de USE PLAN de la consulta.  
  
    2.  Pruebe la consulta.  
  
    3.  Si el optimizador no selecciona un plan adecuado, ajuste la consulta y, a continuación, considere especificar la sugerencia de USE PLAN con el plan de consulta deseado.  
  
     **Cuando se especifica la sugerencia USE PLAN en una guía de plan:**  
  
    1.  Utilice la función sys.fn_validate_plan_guide para comprobar la validez de la guía de plan. O bien, puede comprobar si hay planes no válidos mediante el evento Guía de plan incorrecto de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
    2.  Si la guía de plan no es válida, elimínela. Si el optimizador no selecciona un plan adecuado, ajuste la consulta y, a continuación, considere especificar la sugerencia de USE PLAN con el plan de consulta que desee.  
  
     Un plan que no es válido no hará que la consulta no se pueda ejecutar cuando la sugerencia de USE PLAN se especifique en una guía de plan. En su lugar, la consulta se compila sin utilizar la sugerencia de USE PLAN.  
  
 Las bases de datos marcadas como habilitadas o deshabilitadas para texto completo antes de la actualización conservarán dicho estado tras la actualización. Después de la actualización, los catálogos de texto completo se volverán a generar y a rellenar automáticamente en todas las bases de datos habilitadas para texto completo. Se trata de una operación que consume tiempo y recursos. Puede pausar la operación de indización de texto completo temporalmente ejecutando la siguiente instrucción:  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 1;  
```  
  
 Para reanudar el rellenado de los índices de texto completo, ejecute la siguiente instrucción:  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 0;  
```  
  
## <a name="see-also"></a>Vea también  
 [Actualizaciones de ediciones y versiones admitidas](supported-version-and-edition-upgrades.md)   
 [Trabajar con varias versiones e instancias de SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [Compatibilidad con versiones anteriores](../../getting-started/backward-compatibility.md)   
 [Actualizar bases de datos replicadas](upgrade-replicated-databases.md)  
  
  
