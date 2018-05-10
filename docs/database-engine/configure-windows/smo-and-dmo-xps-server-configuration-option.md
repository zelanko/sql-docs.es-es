---
title: SMO y DMO XPs (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e9ab4a83c9485516a41cb7f38a020d6c6376faae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO and DMO XPs (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>Ver también  
 [Guía de programación para objetos de administración de SQL Server &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
