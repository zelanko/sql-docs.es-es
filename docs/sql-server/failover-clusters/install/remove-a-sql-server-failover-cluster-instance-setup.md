---
title: Eliminación de una instancia de clúster de conmutación por error
description: Use este procedimiento para desinstalar una instancia en clúster de conmutación por error de SQL Server. En este artículo se incluyen consideraciones importantes antes de continuar.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], removing failover clustered instance
- failover clustering [SQL Server], removing failover clustered instance
- uninstalling failover clustered instances
- removing failover clustered instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dba18abbd7eb5938b7f2fa4d0c3caff8d5d6f567
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897677"
---
# <a name="remove-a-sql-server-failover-cluster-instance-setup"></a>Quitar una instancia de clúster de conmutación por error de SQL Server (programa de instalación)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Utilice este procedimiento para desinstalar una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Para actualizar o quitar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es preciso ser administrador local con derecho de iniciar sesión como servicio en todos los nodos del clúster de conmutación por error.  
  
 **Antes de empezar**  
  
 Tenga en cuenta los siguiente puntos importantes antes de desinstalar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   Si se desinstala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client por accidente, se generará un error al iniciar los recursos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para volver a instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para instalar los requisitos previos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Si desinstala un clúster de conmutación por error que tenga más de un recurso de clúster IP de SQL, debe quitar los recursos IP de SQL adicionales mediante el Administrador de clústeres.  
  
 Para obtener más información sobre la sintaxis de la línea de comandos, vea [Instalar SQL Server 2016 desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
### <a name="to-uninstall-a-ssnoversion-failover-cluster"></a>Para desinstalar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Para desinstalar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , utilice la funcionalidad Eliminar nodo proporcionada por el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para quitar cada nodo individualmente. Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
## <a name="see-also"></a>Consulte también  
 [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
