---
title: "Ole Automation Procedures (opción de configuración del servidor) | Microsoft Docs"
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
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a7fc4822969e705f82cf6caa75b893f33e923395
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="ole-automation-procedures-server-configuration-option"></a>Ole Automation Procedures (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use la opción **Ole Automation Procedures** para especificar si se pueden crear instancias de los objetos de automatización OLE en lotes de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esta opción también se puede configurar usando la administración basada en directivas o el procedimiento almacenado **sp_configure** . Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
 La opción **Ole Automation Procedures** se puede establecer con los siguientes valores.  
  
 0  
 Los procedimientos de automatización OLE están deshabilitados. Valor predeterminado para las nuevas sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 1  
 Los procedimientos de automatización OLE están habilitados.  
  
 Cuando los procedimientos de automatización OLE están habilitados, una llamada a **sp_OACreate** iniciará el entorno de ejecución compartido OLE.  
  
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
  
## <a name="see-also"></a>Vea también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Configuración de Área expuesta](../../relational-databases/security/surface-area-configuration.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  

