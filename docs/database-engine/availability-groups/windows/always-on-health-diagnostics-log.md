---
title: Registro de diagnósticos de estado de grupos de disponibilidad Always On (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
caps.latest.revision: 5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 743a80feaa322624ec9fb04111a3b57230d8bbe6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32859880"
---
# <a name="always-on-availability-groups-health-diagnostics-log"></a>Registro de diagnósticos de estado de grupos de disponibilidad Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para supervisar el estado de la réplica de disponibilidad principal, la DLL del recurso de SQL Server ejecutada por el clúster de clústeres de conmutación por error de Windows Server (WSFC) usa un procedimiento almacenado de la instancia de SQL Server denominado [sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md).  
  
 La DLL del recurso de SQL Server mantiene una conexión abierta dedicada con la instancia de SQL Server a través de la que la instancia de SQL Server envía periódicamente diagnósticos de estado detallados a la DLL del recurso de SQL Server. Los diagnósticos de estado, junto con la directiva de conmutación por error configurada en el recurso de grupo de disponibilidad del clúster (la propiedad FailoverConditionLevel), son usados por el clúster para determinar si se debe reiniciar o conmutar por error el recurso de grupo de disponibilidad. Este procedimiento almacenado es la instancia de "latido" de SQL Server 2012 y superior para el clúster WSFC, que es más granular y confiable que en SQL Server 2008 R2 o anterior, donde una conexión periódica a la instancia se establece con la consulta `SELECT @@SERVERNAME`. Luego puede controlar las condiciones que desencadenan las conmutaciones por error al establecer la propiedad FailureConditonLevel del grupo de disponibilidad.  
  
 **Usar los registros de diagnóstico del clúster de conmutación por error de SQL Server**
 
 Todos los diagnósticos de estado que recibe la DLL del recurso de SQL Server desde sp_server_diagnostics se guardan automáticamente en el directorio Log predeterminado de la instancia de SQL Server (%PROGRAMFILES%\Microsoft SQL Server\MSSQL11. MSSQLSERVER\MSSQL\Log). Estos registros se conocen como registros SQLDIAG y se guardan en el formato de archivo XEL (eventos extendidos). Estos archivos del directorio Log de SQL Server tienen el siguiente formato: \<HOSTNAME>_\<INSTANCENAME>_SQLDIAG_X_XXXXXXXXX.xel. Al examinar los registros SQLDIAG, es posible determinar la causa raíz de un error o un evento de conmutación por error del recurso de grupo de disponibilidad.  
  
 Para ver un registro SQLDIAG, arrastre el archivo .xel a SQL Server Management Studio.  
  
  