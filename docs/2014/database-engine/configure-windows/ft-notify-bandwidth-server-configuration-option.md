---
title: ft notify bandwidth (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 375e7c8a1bb520f5a3004c5279682d5b3f145b13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62782500"
---
# <a name="ft-notify-bandwidth-server-configuration-option"></a>ft notify bandwidth (opción de configuración del servidor)
  Utilice la opción **ft notify bandwidth** (ancho de banda de notificación de texto completo) para especificar el tamaño hasta el que pueden crecer los grupos de búferes de memoria pequeños. Los búferes de memoria pequeños tienen un tamaño de 64 kilobytes (KB). El valor del parámetro *max* especifica el número máximo de búferes que debería mantener el administrador de memoria de texto completo en un grupo de búferes pequeño. Si el `max` valor es cero, no hay ningún límite superior para el número de búferes que pueden estar en un grupo de búferes pequeño.  
  
 El parámetro **min** especifica el número mínimo de búferes de memoria que deben mantenerse en el grupo de búferes de memoria pequeños. Tras la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitud del administrador de memoria, se liberarán todos los grupos de búferes adicionales, pero se mantendrá este número mínimo de búferes. Sin embargo, si el valor especificado de **min** es cero, se liberarán todos los búferes de memoria.  
  
 Bajo ciertas circunstancias, el número de búferes asignados actualmente es menor que el valor especificado por el parámetro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [ft Crawl Bandwidth (opción de configuración del servidor)](ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
