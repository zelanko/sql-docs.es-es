---
title: MSSQLSERVER_41030 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41030 (Database Engine error)
ms.assetid: c85341ae-0fbf-42ae-9275-4cfe678238f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b82b11292006be54a2f97c32d4963ea623c6ad02
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85694617"
---
# <a name="mssqlserver_41030"></a>MSSQLSERVER_41030
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|41030|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|OPEN_CLUSTER_SUB_KEY|  
|Texto del mensaje|No se pudo abrir la subclave del Registro '%.*ls' de clústeres de conmutación por error de Windows Server (WSFC) (código de error %d).  La clave principal del clúster es la clave raíz del clúster.  Puede que el servicio WSFC no se esté ejecutando o no esté accesible en su estado actual, o que los argumentos especificados no sean válidos. Si el grupo de disponibilidad correspondiente se ha quitado, este error es previsible. Para obtener más información sobre este código de error, vea "Códigos de error del sistema” en la documentación de Desarrollo en Windows.|  
  
## <a name="explanation"></a>Explicación  
Si se destruye un clúster de WSFC, quita todas las claves del Registro relacionadas con [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
## <a name="user-action"></a>Acción del usuario  
Después de volver crear un clúster de WSFC, deshabilite y vuelva a habilitar AlwaysOn en todos los nodos del clúster en los que haya una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilitada para AlwaysOn. Puede usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para realizar esta tarea.  
  
## <a name="see-also"></a>Consulte también  
[Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
[Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](~/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
