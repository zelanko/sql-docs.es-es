---
title: Ole Automation Procedures (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cb13d9b50c78ff3d067d97b2d5dd1b763e024608
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67997954"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Ole Automation Procedures (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use la opción **Ole Automation Procedures** para especificar si se pueden crear instancias de los objetos de automatización OLE en lotes de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esta opción también se puede configurar usando la administración basada en directivas o el procedimiento almacenado **sp_configure** . Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
 La opción **Ole Automation Procedures** se puede establecer con los siguientes valores.  
  
 0  
 Los procedimientos de automatización OLE están deshabilitados. Valor predeterminado para las nuevas sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 1  
 Los procedimientos de automatización OLE están habilitados.  
  
 Cuando los procedimientos de OLE Automation están habilitados, una llamada a **sp_OACreate** iniciará el entorno de ejecución compartido OLE.  
  
 El valor actual de la opción **Ole Automation Procedures** se puede ver y cambiar con el procedimiento almacenado del sistema **sp_configure** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra cómo se ve la configuración actual de OLE Automation Procedures.  
  
```  
EXEC sp_configure 'Ole Automation Procedures';  
GO  
```  
  
 En el ejemplo siguiente se muestra cómo se habilitan los procedimientos de automatización OLE.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Ole Automation Procedures', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Configuración de Área expuesta](../../relational-databases/security/surface-area-configuration.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
