---
title: Ole Automation Procedures (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a1f1feb6278c36f09c978f5f8f1ae6dbf9f64e60
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205765"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Ole Automation Procedures (opción de configuración del servidor)
  Utilice la opción `Ole Automation Procedures` para especificar si se pueden crear instancias de los objetos de OLE Automation en lotes de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esta opción también se puede configurar usando la administración basada en directivas o el procedimiento almacenado **sp_configure** . Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
 El `Ole Automation Procedures` opción se puede establecer en los siguientes valores.  
  
 0  
 Los procedimientos de automatización OLE están deshabilitados. Valor predeterminado para las nuevas sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 1  
 Los procedimientos de automatización OLE están habilitados.  
  
 Cuando los procedimientos de automatización OLE están habilitados, una llamada a **sp_OACreate** iniciará el entorno de ejecución compartido OLE.  
  
 El valor actual de la `Ole Automation Procedures` se puede ver y cambiar mediante la opción la **sp_configure** procedimiento almacenado del sistema.  
  
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
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Configuración de Área expuesta](../../relational-databases/security/surface-area-configuration.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
