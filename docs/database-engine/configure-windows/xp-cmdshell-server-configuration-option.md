---
title: xp_cmdshell (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6d403205c3fc3ef57fcfa7e566f0913f00604862
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32864320"
---
# <a name="xpcmdshell-server-configuration-option"></a>xp_cmdshell (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  La opción **xp_cmdshell** es una opción de configuración del servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite a los administradores del sistema controlar si el procedimiento almacenado extendido **xp_cmdshell** se puede ejecutar en un sistema. De forma predeterminada, la opción **xp_cmdshell** está deshabilitada en las nuevas instalaciones. Antes de habilitar esta opción, es importante tener en cuenta las posibles implicaciones de seguridad asociadas al uso de esta opción. Esta opción no se debería usar con el código desarrollado recientemente, ya que generalmente debería dejarse deshabilitada. Algunas aplicaciones heredadas requieren que esté habilitada y, si no se pueden modificar para evitar el uso de esta opción, esta puede habilitarse mediante la administración basada en directivas o ejecutando el procedimiento almacenado del sistema **sp_configure**, como se muestra en el ejemplo de código siguiente:  
  
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
  
## <a name="see-also"></a>Ver también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
