---
title: "SMO y DMO XPs (opción de configuración del servidor) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26b79d125d64a1c262c28b71d4c17bbc1824bf6f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO and DMO XPs (opción de configuración del servidor)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Utilice la opción SMO y DMO XPs para habilitar en este servidor los procedimientos almacenados de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO).  
  
 Tenga en cuenta que, a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], DMO se ha quitado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En la siguiente tabla se describen los valores posibles:  
  
|Valor|Significado|  
|-----------|-------------|  
|0|SMO XPs no está disponible.|  
|1|SMO XPs está disponible. Ésta es la opción predeterminada.|  
  
 La configuración surte efecto de forma inmediata.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se habilitan los procedimientos almacenados extendidos de SMO.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Guía de programación para objetos de administración de SQL Server &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
