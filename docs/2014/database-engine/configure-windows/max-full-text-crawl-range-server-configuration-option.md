---
title: max full-text crawl range (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: e1dbd9e44518b6e849a06a76e21fc605172fd2ff
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935220"
---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>max full-text crawl range (opción de configuración del servidor)
  La opción **max full-text crawl range** (tamaño máximo de rastreo de texto completo) sirve para optimizar el uso de la CPU, lo que mejora el rendimiento durante un rastreo completo. Con esta opción, puede especificar el número de particiones que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe usar durante un rastreo de índice completo. Por ejemplo, si hay muchas CPU y su uso no es óptimo, puede aumentar el valor máximo de esta opción. Además de esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza otros factores, como el número de filas de la tabla y el número de CPU, para determinar el número real de particiones utilizadas.  
  
 El valor predeterminado de esta opción es 4, el valor mínimo es 1 y el valor máximo es 256. Los cambios realizados en esta opción solo afectan a los rastreos subsiguientes. Los cambios en la configuración de esta opción no afectarán a los rastreos en curso.  
  
 La opción **max full-text crawl range** es una opción avanzada. Si está usando el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo podrá cambiar el valor de **max full-text crawl range** si **show advanced options** está establecido en 1. La configuración surte efecto inmediatamente, sin necesidad de reiniciar un servidor.  
  
## <a name="see-also"></a>Consulte también  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
