---
title: Información general sobre instrucciones Transact-SQL para grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: f635faa05d7d77a50d31491b1bab9b16875e728c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813828"
---
# <a name="overview-of-transact-sql-statements-for-alwayson-availability-groups-sql-server"></a>Información general sobre instrucciones Transact-SQL para grupos de disponibilidad de AlwaysOn (SQL Server)
  En este tema se presentan las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] que admiten la implementación de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y la creación y administración de un grupo de disponibilidad, réplica de disponibilidad y base de datos de disponibilidad dados.  
  
  
##  <a name="CreateEndpoint"></a> CREATE ENDPOINT  
 [CREATE ENDPOINT ... FOR DATABASE_MIRRORING](/sql/t-sql/statements/create-endpoint-transact-sql) crea un punto de conexión de creación de reflejo de la base de datos si no existe ninguno en la instancia de servidor. Cada instancia de servidor en el que vaya a implementar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] o la creación de reflejo de la base de datos requiere un extremo de creación de reflejo de la base de datos.  
  
 Ejecute esta instrucción en la instancia de servidor en la que se va a crear el extremo. Puede crear solo un extremo de creación de reflejo de la base de datos en una instancia de servidor determinada. Para obtener más información, vea [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
##  <a name="CreateAG"></a> CREATE AVAILABILITY GROUP  
 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql) crea un nuevo grupo de disponibilidad y, opcionalmente, una escucha del grupo de disponibilidad. Como mínimo, debe especificar la instancia del servidor local, que se convertirá en la réplica principal inicial. Opcionalmente, puede especificar también hasta cuatro réplicas secundarias.  
  
 Ejecute CREATE AVAILABILITY GROUP en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que desea hospedar la réplica principal inicial del nuevo grupo de disponibilidad. Esta instancia del servidor debe residir en un nodo de un clúster de conmutación por error de Windows Server (WSFC) (para obtener más información, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="AlterAG"></a> ALTER AVAILABILITY GROUP  
 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) admite el cambio de un grupo de disponibilidad existente o una escucha de grupo de disponibilidad y la conmutación por error en un grupo de disponibilidad.  
  
 Ejecute ALTER AVAILABILITY GROUP en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda la réplica principal actual.  
  
##  <a name="AlterDb"></a> ALTER DATABASE ... SET HADR ...  
 Las opciones de la cláusula [SET HADR](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) de la instrucción ALTER DATABASE permiten combinar una base de datos secundaria con el grupo de disponibilidad de la base de datos principal correspondiente, quitar una base de datos combinada y suspender la sincronización de datos en una base de datos combinada, y reanudar la sincronización de datos.  
  
##  <a name="DropAG"></a> DROP AVAILABILITY GROUP  
 [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) quita un grupo de disponibilidad especificado y todas sus réplicas. DROP AVAILABILITY GROUP se puede ejecutar desde cualquier nodo de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] del clúster de conmutación por error de WSFC.  
  
##  <a name="Restrictions"></a> Restricciones de las instrucciones AVAILABILITY GROUP de Transact-SQL  
 Las instrucciones CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP y DROP AVAILABILITY GROUP de [!INCLUDE[tsql](../../../includes/tsql-md.md)] tienen las siguientes restricciones:  
  
-   Excepto en DROP AVAILABILITY GROUP, la ejecución de estas instrucciones requiere que el servicio HADR esté habilitado en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   Estas instrucciones no se pueden ejecutar en transacciones o por lotes.  
  
-   Aunque llevan a cabo el máximo de acciones para efectuar la limpieza después de un error, estas instrucciones no garantizan que revertirán todos los cambios al producirse un error. No obstante, los sistemas se deben controlar correctamente y, a continuación, ignorar los errores parciales.  
  
-   Estas instrucciones no admiten expresiones o variables.  
  
-   Si se ejecuta una instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] mientras está en curso otra acción o recuperación de grupo de disponibilidad, la instrucción devuelve un error. Espere a que se complete la acción o la recuperación, e intente de nuevo la instrucción, si es necesario.  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
