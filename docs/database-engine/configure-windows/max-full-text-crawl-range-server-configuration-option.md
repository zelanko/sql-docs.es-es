---
title: max full-text crawl range (opción de configuración del servidor) | Microsoft Docs
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
- crawls [full-text search]
- max full-text crawl range option
ms.assetid: a49de86b-0891-4dcd-89c0-ead30aab00e0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 740d952640cef0400c379e9dfb25157331c9bfab
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68023754"
---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>max full-text crawl range (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  La opción **max full-text crawl range** (tamaño máximo de rastreo de texto completo) sirve para optimizar el uso de la CPU, lo que mejora el rendimiento durante un rastreo completo. Con esta opción, puede especificar el número de particiones que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe usar durante un rastreo de índice completo. Por ejemplo, si hay muchas CPU y su uso no es óptimo, puede aumentar el valor máximo de esta opción. Además de esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza otros factores, como el número de filas de la tabla y el número de CPU, para determinar el número real de particiones utilizadas.  
  
 El valor predeterminado de esta opción es 4, el valor mínimo es 1 y el valor máximo es 256. Los cambios realizados en esta opción solo afectan a los rastreos subsiguientes. Los cambios en la configuración de esta opción no afectarán a los rastreos en curso.  
  
 La opción **max full-text crawl range** es una opción avanzada. Si está usando el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo podrá cambiar el valor de **max full-text crawl range** si **show advanced options** está establecido en 1. La configuración surte efecto inmediatamente, sin necesidad de reiniciar un servidor.  
  
## <a name="see-also"></a>Consulte también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
