---
title: Configurar FILESTREAM en un clúster de conmutación por error | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], setting up on a failover cluster
ms.assetid: 6721f780-20b7-4109-8ddb-ac327310699e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9357a345593cd81c420b702a38a02c60da5aebcc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66009922"
---
# <a name="set-up-filestream-on-a-failover-cluster"></a>Configurar FILESTREAM en un clúster de conmutación por error
  En este tema se describe cómo habilitar FILESTREAM en un clúster de conmutación por error. Antes de probar este procedimiento, debería conocer los [clústeres de conmutación por error](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) y tener habilitado FILESTREAM. Para obtener información sobre cómo habilitar FILESTREAM, vea [Habilitar y configurar FILESTREAM](enable-and-configure-filestream.md).  
  
### <a name="to-set-up-filestream-on-a-failover-cluster"></a>Para configurar FILESTREAM en un clúster de conmutación por error  
  
1.  Configure el nodo principal para el clúster de conmutación por error.  
  
     Cuando finalice el programa de instalación, habilite FILESTREAM en el nodo principal utilizando **Administrador de configuración de SQL Server**. De este modo habilita la configuración que requiere los privilegios de administrador de Windows. Si se requiere acceso remoto, seleccione **Permitir que los clientes remotos tengan acceso de transmisión por secuencias a los datos de FILESTREAM**. De esta forma creará un recurso de clúster de recurso compartido de archivos.  
  
2.  Configure un nodo pasivo.  
  
     Cuando finalice el programa de instalación, habilite FILESTREAM en el nodo pasivo utilizando **Administrador de configuración de SQL Server**. El nombre que especifica para **Nombre de recurso compartido de Windows** debe ser el mismo en todos los nodos del clúster.  
  
3.  Repita el paso 2 para agregar más nodos pasivos.  
  
4.  Una vez agregados todos los nodos, complete el proceso ejecutando el procedimiento almacenado sp_configure en cada sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Puede repetir los pasos 2, 3 y 4 para agregar y habilitar nodos adicionales en el clúster en cualquier momento.  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Crear un nuevo clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [Quitar una instancia de clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)   
 [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
  
