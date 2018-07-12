---
title: max full-text crawl range (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- crawls [full-text search]
- max full-text crawl range option
ms.assetid: a49de86b-0891-4dcd-89c0-ead30aab00e0
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e564a81b9466750e882d4ebe19604deb92f87e34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37156826"
---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>max full-text crawl range (opción de configuración del servidor)
  La opción **max full-text crawl range** (tamaño máximo de rastreo de texto completo) sirve para optimizar el uso de la CPU, lo que mejora el rendimiento durante un rastreo completo. Con esta opción, puede especificar el número de particiones que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe utilizar durante un rastreo de índice completo. Por ejemplo, si hay muchas CPU y su uso no es óptimo, puede aumentar el valor máximo de esta opción. Además de esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza otros factores, como el número de filas de la tabla y el número de CPU, para determinar el número real de particiones utilizadas.  
  
 El valor predeterminado de esta opción es 4, el valor mínimo es 1 y el valor máximo es 256. Los cambios realizados en esta opción solo afectan a los rastreos subsiguientes. Los cambios en la configuración de esta opción no afectarán a los rastreos en curso.  
  
 La opción **max full-text crawl range** es una opción avanzada. Si está usando el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo podrá cambiar el valor de **max full-text crawl range** si **show advanced options** está establecido en 1. La configuración surte efecto inmediatamente, sin necesidad de reiniciar un servidor.  
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
