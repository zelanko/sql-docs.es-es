---
title: "Creación de reflejo de la base de datos - Grupos de disponibilidad AlwaysOn - PowerShell | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], endpoint
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7de2f3f143cd5bc800493034f2abf7aed925b7a3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="database-mirroring---always-on-availability-groups--powershell"></a>Creación de reflejo de la base de datos - Grupos de disponibilidad AlwaysOn - PowerShell
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo crear un extremo de creación de reflejo de la base de datos para uso de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante PowerShell.  
  
 **En este tema**  
  
-   **Antes de empezar:**  [Seguridad](#Security)  
  
-   **Para crear un extremo de creación de reflejo de la base de datos utilizando:**  [PowerShell](#PowerShellProcedure)  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
> [!IMPORTANT]  
>  El algoritmo RC4 está obsoleto. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] Se recomienda utilizar AES.  
  
####  <a name="Permissions"></a> Permisos  
 Requiere permiso CREATE ENDPOINT o pertenecer al rol fijo de servidor sysadmin. Para obtener más información, vea [GRANT &#40;permisos de punto de conexión de Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para crear un extremo de creación de reflejo de la base de datos**  
  
1.  Cambie el directorio (**cd**) a la instancia del servidor para la que quiera crear el punto de conexión de creación de reflejo de la base de datos.  
  
2.  Use el cmdlet **New-SqlHadrEndpoint** para crear el punto de conexión y, después, use **Set-SqlHadrEndpoint** para iniciarlo.  
  
###  <a name="PShellExample"></a> Ejemplo (PowerShell)  
 Los siguientes comandos de PowerShell crean un punto de conexión de creación de reflejo de la base de datos en una instancia de SQL Server (*Machine*\\*Instance*). El extremo utiliza el puerto 5022.  
  
> [!IMPORTANT]  
>  Este ejemplo solamente funciona en una instancia de servidor que no disponga actualmente de un extremo de creación de reflejo de la base de datos.  
  
```  
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"  
  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar un extremo de creación del reflejo de la base de datos**  
  
-   [Crear un punto de conexión de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Permitir que un punto de conexión de creación de reflejo de la base de datos utilice certificados para las conexiones salientes &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Permitir que un punto de conexión de creación de reflejo de la base de datos use certificados para las conexiones entrantes &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Especificar una dirección de red de servidor &#40;creación de reflejo de la base de datos&#41;](../../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Para ver información acerca del extremo de creación de reflejo de la base de datos**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear un grupo de disponibilidad &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
