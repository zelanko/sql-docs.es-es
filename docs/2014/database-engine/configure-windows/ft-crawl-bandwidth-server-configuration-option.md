---
title: ft crawl bandwidth (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 34ae9ddc8f9b2626ecf51f917a4f6cd345f6bb06
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214445"
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>ft crawl bandwidth (opción de configuración del servidor)
  Utilice la opción **ft crawl bandwidth** (ancho de banda de notificación de texto completo) para especificar el tamaño hasta donde puede crecer un grupo de búferes de memoria de gran tamaño. Los búferes de memoria de gran tamaño tienen 4 MB. El valor del parámetro **max** especifica el máximo de búferes que debe mantener el administrador de memoria de texto completo en un grupo de búferes de gran tamaño. Si el valor de **max** es cero, no habrá ningún límite superior para el número de búferes que pueden estar en un grupo de búferes de gran tamaño.  
  
 El parámetro **min** especifica el número mínimo de búferes de memoria que deben mantenerse en el grupo de búferes de memoria de gran tamaño. A solicitud del administrador de memoria de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se liberarán todos los grupos de búferes adicionales, pero se mantendrá este número mínimo de búferes. Sin embargo, si el valor especificado de **min** es cero, se liberarán todos los búferes de memoria.  
  
 Bajo ciertas circunstancias, el número de búferes asignados actualmente es menor que el valor especificado por el parámetro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Opción de configuración del servidor Ancho de banda para notificación de texto completo](ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
