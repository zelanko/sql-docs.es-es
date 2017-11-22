---
title: "access check cache (opciones de configuración del servidor) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 484e995a5b9c99fdc2a6a13cc2f5278cc0d968cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="access-check-cache-server-configuration-options"></a>access check cache (opciones de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tiene acceso a los objetos de base de datos, la comprobación del acceso se almacena en memoria caché en una estructura interna denominada **memoria caché de resultados de comprobación de acceso**. Las opciones **access check cache quota** y **access check cache bucket count** controlan el número de entradas y de depósitos de hash que se usan para **access check result cache**. En circunstancias excepcionales, el rendimiento se puede mejorar cambiando estas opciones.  
  
 Los valores predeterminados de 0 indican que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está administrando estas opciones. Microsoft solo recomienda cambiar estas opciones cuando lo indiquen los servicios de soporte al cliente de Microsoft.  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
