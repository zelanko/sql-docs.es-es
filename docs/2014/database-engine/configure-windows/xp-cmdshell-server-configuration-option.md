---
title: xp_cmdshell (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5db62cf5c549d4bfbea98a6584f91171bd93afa7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201206"
---
# <a name="xpcmdshell-server-configuration-option"></a>xp_cmdshell (opción de configuración del servidor)
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
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  