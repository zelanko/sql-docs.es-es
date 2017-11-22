---
title: dbo.server_quotas (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/02/2016
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs: TSQL
helpviewer_keywords: server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 612f4d0a819c1271ca9b5e8b9fda8f224ae6fbe6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **IMPORTANTE:** Esto se aplica a  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 solo!**  
>   
>  Esta característica se encuentra en un estado de vista previa. No dependa de la implementación específica de esta característica, ya que podría modificarse o quitarse en una versión futura.  
  
 Devuelve los tipos de cuota de base de datos disponibles en el servidor.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|El tipo de cuota del servidor. El tipo **Premium_database** es equivalente a las bases de datos con una reserva de recursos.|  
|quota_value|**int**|El número de tipo de cuota permitido en el servidor.|  
  
## <a name="permissions"></a>Permissions  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a virtual **maestro** base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Administración de bases de datos Premium](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
