---
title: ft crawl bandwidth (opción de configuración del servidor) | Microsoft Docs
description: Obtenga información sobre la opción "ft crawl bandwidth". Vea cómo afecta al número de búferes que SQL Server mantiene en el grupo de búferes de memoria de gran tamaño.
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
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 59caa1e868c4caab24afd17909c34f57c96f0005
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789789"
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>ft crawl bandwidth (opción de configuración del servidor)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Utilice la opción **ft crawl bandwidth** (ancho de banda de notificación de texto completo) para especificar el tamaño hasta donde puede crecer un grupo de búferes de memoria de gran tamaño. Los búferes de memoria de gran tamaño tienen 4 MB. El valor del parámetro **max** especifica el máximo de búferes que debe mantener el administrador de memoria de texto completo en un grupo de búferes de gran tamaño. Si el valor de **max** es cero, no habrá ningún límite superior para el número de búferes que pueden estar en un grupo de búferes de gran tamaño.  
  
 El parámetro **min** especifica el número mínimo de búferes de memoria que deben mantenerse en el grupo de búferes de memoria de gran tamaño. Previa solicitud del administrador de memoria de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se liberan todos los grupos de búferes adicionales, aunque se mantiene este número mínimo de búferes. Sin embargo, si el valor especificado de **min** es cero, se liberarán todos los búferes de memoria.  
  
 Bajo ciertas circunstancias, el número de búferes asignados actualmente es menor que el valor especificado por el parámetro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Opción de configuración del servidor Ancho de banda para notificación de texto completo](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
