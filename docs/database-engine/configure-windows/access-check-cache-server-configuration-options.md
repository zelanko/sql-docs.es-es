---
title: access check cache (opciones de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 075cd37a349ea8d3900a235843657d89b71e8739
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763933"
---
# <a name="access-check-cache-server-configuration-options"></a>access check cache (opciones de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tiene acceso a los objetos de base de datos, la comprobación del acceso se almacena en memoria caché en una estructura interna denominada **memoria caché de resultados de comprobación de acceso**. Las opciones **access check cache quota** y **access check cache bucket count** controlan el número de entradas y de cubos de hash que se usan para **access check result cache**. En circunstancias excepcionales, el rendimiento se puede mejorar cambiando estas opciones.  
  
 Los valores predeterminados de 0 indican que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está administrando estas opciones. Microsoft solo recomienda cambiar estas opciones cuando lo indiquen los servicios de soporte al cliente de Microsoft.  
  
## <a name="see-also"></a>Ver también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
