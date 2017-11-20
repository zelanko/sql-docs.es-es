---
title: "xp_cmdshell (opción de configuración del servidor) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b32eef170d0834b44932f753075bbd2df67762a2
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="xpcmdshell-server-configuration-option"></a>xp_cmdshell (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  La opción **xp_cmdshell** es una opción de configuración del servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite a los administradores del sistema controlar si el procedimiento almacenado extendido **xp_cmdshell** se puede ejecutar en un sistema. La opción **xp_cmdshell** está deshabilitada de forma predeterminada en las instalaciones nuevas y se puede habilitar mediante Administración basada en directivas o ejecutando el procedimiento almacenado del sistema **sp_configure** , tal y como se muestra en el ejemplo de código siguiente:  
  
```  
-- To allow advanced options to be changed.  
EXEC sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXEC sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  

