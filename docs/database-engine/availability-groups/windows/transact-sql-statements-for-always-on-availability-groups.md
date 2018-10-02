---
title: Instrucciones Transact-SQL para grupos de disponibilidad AlwaysOn | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: 184d0a81-2259-4db9-9d0d-01aac0b502c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9711abe965e293824da78bf0d956311679fc7c9f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771429"
---
# <a name="transact-sql-statements-for-always-on-availability-groups"></a>Instrucciones Transact-SQL para grupos de disponibilidad AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se presentan las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] que admiten la implementación de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y la creación y administración de un grupo de disponibilidad, réplica de disponibilidad y base de datos de disponibilidad dados.  
  
 **En este tema:**  
  
-   [CREATE ENDPOINT](#CreateEndpoint)  
  
-   [CREATE AVAILABILITY GROUP](#CreateAG)  
  
-   [ALTER AVAILABILITY GROUP](#AlterAG)  
  
-   [Opciones de ALTER DATABASE SET HADR](#AlterDb)  
  
-   [DROP AVAILABILITY GROUP](#DropAG)  
  
-   [Restricciones de las instrucciones AVAILABILITY GROUP de Transact-SQL](#Restrictions)  
  
##  <a name="CreateEndpoint"></a> CREATE ENDPOINT  
 [CREATE ENDPOINT … FOR DATABASE_MIRRORING](../../../t-sql/statements/create-endpoint-transact-sql.md) crea un punto de conexión de creación de reflejo de la base de datos si no existe ninguno en la instancia de servidor. Cada instancia de servidor en el que vaya a implementar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] o la creación de reflejo de la base de datos requiere un extremo de creación de reflejo de la base de datos.  
  
 Ejecute esta instrucción en la instancia de servidor en la que se va a crear el extremo. Puede crear solo un extremo de creación de reflejo de la base de datos en una instancia de servidor determinada. Para obtener más información, vea [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
##  <a name="CreateAG"></a> CREATE AVAILABILITY GROUP  
 [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md) crea un nuevo grupo de disponibilidad y, opcionalmente, una escucha del grupo de disponibilidad. Como mínimo, debe especificar la instancia del servidor local, que se convertirá en la réplica principal inicial. Opcionalmente, puede especificar también hasta cuatro réplicas secundarias.  
  
 Ejecute CREATE AVAILABILITY GROUP en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que desea hospedar la réplica principal inicial del nuevo grupo de disponibilidad. Esta instancia de servidor debe residir en un nodo de un clúster de conmutación por error de Windows Server (WSFC). Para obtener más información, vea [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="AlterAG"></a> ALTER AVAILABILITY GROUP  
 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) admite el cambio de un grupo de disponibilidad existente o una escucha de grupo de disponibilidad y la conmutación por error en un grupo de disponibilidad.  
  
 Ejecute ALTER AVAILABILITY GROUP en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda la réplica principal actual.  
  
##  <a name="AlterDb"></a> ALTER DATABASE … SET HADR …  
 Las opciones de la cláusula [SET HADR](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md) de la instrucción ALTER DATABASE permiten combinar una base de datos secundaria con el grupo de disponibilidad de la base de datos principal correspondiente, quitar una base de datos combinada y suspender la sincronización de datos en una base de datos combinada, y reanudar la sincronización de datos.  
  
##  <a name="DropAG"></a> DROP AVAILABILITY GROUP  
 [DROP AVAILABILITY GROUP](../../../t-sql/statements/drop-availability-group-transact-sql.md) quita un grupo de disponibilidad especificado y todas sus réplicas. DROP AVAILABILITY GROUP se puede ejecutar desde cualquier nodo de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] del clúster de conmutación por error de WSFC.  
  
##  <a name="Restrictions"></a> Restrictions on the AVAILABILITY GROUP Transact-SQL Statements  
 Las instrucciones CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP y DROP AVAILABILITY GROUP de [!INCLUDE[tsql](../../../includes/tsql-md.md)] tienen las siguientes restricciones:  
  
-   Excepto en DROP AVAILABILITY GROUP, la ejecución de estas instrucciones requiere que el servicio HADR esté habilitado en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   Estas instrucciones no se pueden ejecutar en transacciones o por lotes.  
  
-   Aunque llevan a cabo el máximo de acciones para efectuar la limpieza después de un error, estas instrucciones no garantizan que revertirán todos los cambios al producirse un error. No obstante, los sistemas se deben controlar correctamente y, a continuación, ignorar los errores parciales.  
  
-   Estas instrucciones no admiten expresiones o variables.  
  
-   Si se ejecuta una instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] mientras está en curso otra acción o recuperación de grupo de disponibilidad, la instrucción devuelve un error. Espere a que se complete la acción o la recuperación, e intente de nuevo la instrucción, si es necesario.  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
