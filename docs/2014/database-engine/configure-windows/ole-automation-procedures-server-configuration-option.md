---
title: Ole Automation Procedures (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f00c238dfb32089261c51936b3937b0657c58b08
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62782033"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Ole Automation Procedures (opción de configuración del servidor)
  Utilice la opción `Ole Automation Procedures` para especificar si se pueden crear instancias de los objetos de OLE Automation en lotes de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esta opción también se puede configurar usando la administración basada en directivas o el procedimiento almacenado **sp_configure** . Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
 La opción `Ole Automation Procedures` se puede establecer con los siguientes valores.  
  
 0  
 Los procedimientos de automatización OLE están deshabilitados. Valor predeterminado para las nuevas sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 1  
 Los procedimientos de automatización OLE están habilitados.  
  
 Cuando los procedimientos de OLE Automation están habilitados, una llamada a **sp_OACreate** iniciará el entorno de ejecución compartido OLE.  
  
 El valor actual de la `Ole Automation Procedures` opción se puede ver y cambiar mediante el **sp_configure** procedimiento almacenado del sistema.  
  
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
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Configuración de Área expuesta](../../relational-databases/security/surface-area-configuration.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
