---
title: "Agregar conmutación por error de base de datos mejorada a un grupo de disponibilidad (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], enhanced database failover
- Availability Groups [SQL Server], failover
ms.assetid: 
caps.latest.revision: 
author: allanhirt
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0463d237614b25667c8402da70b7c5e4217d4ef5
ms.openlocfilehash: 6faff6e4464f21503132c72034535d11b8c3a0eb
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---

# <a name="add-enhanced-database-failover-to-an-availability-group-sql-server"></a>Agregar conmutación por error de base de datos mejorada a un grupo de disponibilidad (SQL Server)

En SQL Server 2012 y 2014, si una base de datos que participa en un grupo de disponibilidad en la réplica principal pierde la capacidad para escribir transacciones, no desencadenará una conmutación por error, aun cuando las réplicas estén sincronizadas y configuradas para la conmutación automática por error.

SQL Server 2016 incorpora un nuevo comportamiento opcional denominado *conmutación por error de base de datos mejorada* que se puede configurar con el asistente o a través de Transact-SQL. Si esta opción está habilitada y la conmutación automática por error está configurada, cuando una base de datos que participa en un grupo de disponibilidad ya no pueda escribir transacciones, se desencadenará una conmutación por error a una réplica secundaria sincronizada.

**Escenario 1**

Hay un grupo de disponibilidad configurado entre la instancia A y la instancia B que contiene una sola base de datos llamada DB1. El archivo de datos de DB1 está en la unidad de disco E y su archivo de registro de transacciones, en la unidad F. El modo de disponibilidad está establecido en confirmación sincrónica con conmutación automática por error. La nueva opción de conmutación por error de base de datos mejorada está configurada en el grupo de disponibilidad. Las dos réplicas tienen actualmente un estado sincronizado. Un problema hace que la unidad E deje de funcionar. En este escenario no se producirá una conmutación por error de base de datos mejorada, porque la unidad E no contiene el registro de transacciones.  

**Escenario 2**

Tenemos la misma configuración de grupos de disponibilidad que en el escenario 1. En lugar de en la unidad E, esta vez el error se produce en la unidad del registro de transacciones, la unidad F. Esto desencadenará una conmutación por error, dado que se cumple la condición de conmutación por error de base de datos mejorada: el registro de transacciones no está accesible, lo que significa que la base de datos no puede escribir transacciones.

**Escenario 3**

Hay un grupo de disponibilidad configurado entre la instancia A y la instancia B que contiene dos bases de datos: DB1 y DB2. El modo de disponibilidad está establecido en confirmación sincrónica y el modo de conmutación por error, en automático. La conmutación por error de base de datos mejorada está habilitada. Se pierde el acceso al disco que contiene los archivos de registro de transacciones y los datos de DB2. Cuando el problema se detecte, el grupo de disponibilidad conmutará por error automáticamente a la instancia B.

## <a name="configuring-and-viewing-the-enhanced-database-failover-option"></a>Configurar y ver la opción de conmutación por error de base de datos mejorada

La conmutación por error de base de datos mejorada se puede configurar a través de SQL Server Management Studio o de Transact-SQL. Actualmente, esto no se puede realizar con cmdlets de PowerShell. La conmutación por error de base de datos mejorada está deshabilitada de forma predeterminada.

### <a name="sql-server-management-studio"></a>SQL Server Management Studio

La conmutación por error de base de datos mejorada se puede habilitar durante el proceso de creación de un grupo de accesibilidad con SQL Server Management Studio. La única manera de deshabilitarla o habilitarla después de crear el grupo de disponibilidad es por medio de Transact-SQL.

*Creación manual de grupos de disponibilidad*

Use las instrucciones que encontrará en el tema [Usar el cuadro de diálogo Nuevo grupo de disponibilidad (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md) para crear el grupo de disponibilidad. Para habilitar la conmutación por error de base de datos mejorada, active la casilla junto a *Detección del estado del nivel de base de datos*.

*Usar el Asistente para grupo de disponibilidad*

Use las instrucciones que encontrará en el tema [Usar el Asistente para grupo de disponibilidad (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md). La opción para habilitar la conmutación por error de base de datos mejorada se encuentra en el cuadro de diálogo Especificar nombre de grupo de disponibilidad. Para habilitarla, active la casilla junto a *Detección del estado del nivel de base de datos*.

### <a name="transact-sql"></a>Transact-SQL

Para configurar el comportamiento de la conmutación por error de base de datos mejorada durante la creación de un grupo de disponibilidad, DB_FAILOVER debe establecerse en ON como se indica a continuación:
```
CREATE AVAILABILITY GROUP [AGNAME]
WITH ( DB_FAILOVER = ON)
...
```
Para agregar este comportamiento después de configurar un grupo de disponibilidad, use el comando ALTER AVAILABILITY GROUP:
```
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = ON)
```
Para deshabilitar este comportamiento, emita el siguiente comando ALTER AVAILABILITY GROUP:
```
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = OFF)
```
### <a name="dynamic-management-view"></a>Vista de administración dinámica
Para saber si un grupo de disponibilidad tiene habilitada la conmutación por error de base de datos mejorada, realice una consulta a la vista de administración dinámica `sys.availablity_groups`. La columna `db_failover` tendrá un cero si está deshabilitada o 1 si está habilitada. 

## <a name="next-steps"></a>Pasos siguientes 

- [Configurar la detección de mantenimiento de bases de datos](sql-server-always-on-database-health-detection-failover-option.md)

- [Usar el Asistente para grupo de disponibilidad (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

- [Usar el cuadro de diálogo Nuevo grupo de disponibilidad (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
- [Crear un grupo de disponibilidad (Transact-SQL)](create-an-availability-group-transact-sql.md)


