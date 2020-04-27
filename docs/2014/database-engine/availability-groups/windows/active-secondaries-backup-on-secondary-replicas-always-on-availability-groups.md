---
title: 'Secundarias activas: copia de seguridad en las réplicas secundarias (Always On grupos de disponibilidad) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a94db154042f2cc6314459b6af4b52a43c2c9966
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62790684"
---
# <a name="active-secondaries-backup-on-secondary-replicas-always-on-availability-groups"></a>Secundarias activas: copia de seguridad en las réplicas secundarias (grupos de disponibilidad AlwaysOn)
  Las funciones secundarias activas de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] incluyen compatibilidad para realizar operaciones de copia de seguridad en las réplicas secundarias. Las operaciones de copia de seguridad pueden provocar una demanda significativa de E/S y CPU (con la compresión de copia de seguridad). La descarga de las copias de seguridad en una réplica secundaria sincronizada o en proceso de sincronización permite utilizar los recursos de la instancia del servidor que hospeda la réplica principal para las cargas de trabajo de nivel 1.  
  
> [!NOTE]  
>  Las instrucciones RESTORE no se permiten en las bases de datos principales o secundarias de un grupo de disponibilidad.  
  
  
  
##  <a name="backup-types-supported-on-secondary-replicas"></a><a name="SupportedBuTypes"></a>Tipos de copia de seguridad admitidos en las réplicas secundarias  
  
-   `BACKUP DATABASE` solo admite copias de seguridad completas de solo copia de bases de datos, archivos o grupos de archivos cuando se ejecuta en réplicas secundarias. Tenga en cuenta que las copias de seguridad de solo copia no afectan a la cadena de registros ni borran el mapa de bits diferencial.  
  
-   Las copias de seguridad diferenciales no se admiten en las réplicas secundarias.  
  
-   **BACKUP LOG** solo admite copias de seguridad de registros periódicas (la opción COPY_ONLY no se admite para las copias de seguridad de registros en réplicas secundarias).  
  
     Se garantiza una cadena de registro coherente entre las copias de seguridad de registros realizaron en cualquiera de las réplicas (principal o secundaria), con independencia de su modo de disponibilidad (confirmación sincrónica o asincrónica).  
  
-   Para realizar una copia de seguridad de una base de datos secundaria, una réplica secundaria debe poder comunicarse con la réplica principal y su estado debe ser `SYNCHRONIZED` o `SYNCHRONIZING`.  
  
##  <a name="configuring-where-backup-jobs-run"></a><a name="WhereBuJobsRun"></a>Configurar dónde se ejecutan los trabajos de copia de seguridad  
 La realización de copias de seguridad en una réplica secundaria para descargar la carga de trabajo de copias de seguridad del servidor de producción principal es un gran ventaja. Sin embargo, realizar copias de seguridad en réplicas secundarias agrega una gran complejidad al proceso de determinar dónde deben ejecutarse los trabajos de copia de seguridad. Para solucionar este problema, configure dónde se han de ejecutar los trabajos de copia de seguridad del modo siguiente:  
  
1.  Configure el grupo de disponibilidad para que se especifiquen las réplicas de disponibilidad donde preferiría que se realizasen las copias de seguridad. Para obtener más información, vea los parámetros *AUTOMATED_BACKUP_PREFERENCE* y *BACKUP_PRIORITY* en [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql) o [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql).  
  
2.  Cree los trabajos de copia de seguridad incluidos en script para cada base de datos de disponibilidad de cada instancia de servidor que hospeda una réplica de disponibilidad que es candidata para realizar copias de seguridad. Para obtener más información, vea la sección "Seguimiento: después de configurar la copia de seguridad en las réplicas secundarias" de [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar la copia de seguridad en las réplicas secundarias**  
  
-   [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
 **Para determina sir la réplica actual es la réplica de copia de seguridad preferida**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
  
 **Para crear un trabajo de copia de seguridad**  
  
-   [Usar el Asistente para planes de mantenimiento](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [Implementar trabajos](../../../ssms/agent/implement-jobs.md)  
  
  
## <a name="see-also"></a>Consulte también  
 [Información general de Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Copias de seguridad de solo copia &#40;SQL Server&#41;](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [Crear grupo de disponibilidad &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)  
  
  
