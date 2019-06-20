---
title: Quitar una instancia de clúster de conmutación por error de SQL Server (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], removing failover clustered instance
- failover clustering [SQL Server], removing failover clustered instance
- uninstalling failover clustered instances
- removing failover clustered instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07b57b7ebea8a2bf5eaf381c09d7eb29dd6a4cd4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63017030"
---
# <a name="remove-a-sql-server-failover-cluster-instance-setup"></a>Quitar una instancia de clúster de conmutación por error de SQL Server (programa de instalación)
  Utilice este procedimiento para desinstalar una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Para actualizar o quitar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es preciso ser administrador local con derecho de iniciar sesión como servicio en todos los nodos del clúster de conmutación por error.  
  
 **Antes de empezar**  
  
 Tenga en cuenta los siguiente puntos importantes antes de desinstalar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   Si se desinstala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client por accidente, se generará un error al iniciar los recursos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para volver a instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para instalar los requisitos previos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Si desinstala un clúster de conmutación por error que tenga más de un recurso de clúster IP de SQL, debe quitar los recursos IP de SQL adicionales mediante el Administrador de clústeres.  
  
 Para obtener información sobre la sintaxis de línea de comandos, consulte [instalar SQL Server 2014 desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
### <a name="to-uninstall-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Para desinstalar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Para desinstalar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], utilice la funcionalidad Eliminar nodo proporcionada por el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para quitar cada nodo individualmente. Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
## <a name="see-also"></a>Vea también  
 [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
