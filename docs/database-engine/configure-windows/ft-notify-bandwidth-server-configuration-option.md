---
title: ft notify bandwidth (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- ft notify bandwidth opion
- small memory buffers
- memory [SQL Server], buffers
ms.assetid: 9ca284c5-f3e0-4a67-a132-fff376ff0ffe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e4264e97883665ddf845a95a98f3728527a48381
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669183"
---
# <a name="ft-notify-bandwidth-server-configuration-option"></a>ft notify bandwidth (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice la opción **ft notify bandwidth** (ancho de banda de notificación de texto completo) para especificar el tamaño hasta el que pueden crecer los grupos de búferes de memoria pequeños. Los búferes de memoria pequeños tienen un tamaño de 64 kilobytes (KB). El valor del parámetro *max* especifica el número máximo de búferes que debería mantener el administrador de memoria de texto completo en un grupo de búferes pequeño. Si el valor de **max** es cero, no habrá ningún límite superior para el número de búferes que pueden estar en un grupo de búferes pequeños.  
  
 El parámetro **min** especifica el número mínimo de búferes de memoria que deben mantenerse en el grupo de búferes de memoria pequeños. A solicitud del administrador de memoria de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se liberarán todos los grupos de búferes adicionales, pero se mantendrá este número mínimo de búferes. Sin embargo, si el valor especificado de **min** es cero, se liberarán todos los búferes de memoria.  
  
 Bajo ciertas circunstancias, el número de búferes asignados actualmente es menor que el valor especificado por el parámetro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ft crawl bandwidth (opción de configuración del servidor)](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
