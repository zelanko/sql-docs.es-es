---
title: lightweight pooling (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default lightweight pooling
- decreasing overhead
- lightweight pooling option
- system overhead [SQL Server]
- performance [SQL Server], lightweight pooling
- context switching [SQL Server], lightweight pooling option
- excessive context switching [SQL Server]
- reducing overhead
- overhead [SQL Server]
ms.assetid: 2dc11b61-d065-4126-8e00-acf40390f9fb
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: ea3ef8aa6e667935ea65c619221bfbbd10199e99
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785166"
---
# <a name="lightweight-pooling-server-configuration-option"></a>lightweight pooling (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use la opción **agrupación ligera** para proporcionar un medio de reducir la sobrecarga del sistema asociada al cambio de contexto excesivo que se puede observar a veces en entornos con multiprocesadores simétricos (SMP). Cuando hay un cambio de contexto excesivo, la opción de agrupación ligera puede proporcionar un mayor rendimiento al realizar el cambio de contexto insertado, lo que ayuda a reducir las transiciones de llamadas entre el usuario y el kernel.  
  
 El modo de fibra se destina a determinadas situaciones en las que el cambio de contexto de los trabajadores de UMS es un cuello de botella decisivo para el rendimiento. Al ser esta situación inusual, el modo de fibra rara vez mejora el rendimiento o la escalabilidad en el sistema típico. El cambio de contexto mejorado en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] también ha reducido la necesidad del modo de fibra. No se recomienda utilizar la programación en modo de fibra para un funcionamiento habitual. La razón es que puede reducir el rendimiento al impedir las ventajas normales del cambio de contexto, y que algunos componentes de porque algunos componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que utiliza Subproceso Almacenamiento Local (TLS) o los objetos poseídos por subproceso, como exclusiones mutuas (un tipo de objeto de kernel de Win32), no pueden funcionar correctamente en modo de fibra.  
  
 Si establece el valor 1 para **agrupación ligera** , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cambiará a la programación en modo de fibra. El valor predeterminado para esta opción es 0.  
  
 **Agrupación ligera** es una opción avanzada. Si está usando el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo podrá cambiar el valor de **agrupación ligera** si **Mostrar opciones avanzadas** está establecido en 1. La configuración surte efecto cuando se reinicia el servidor.  
  
> [!NOTE]  
>  La agrupación ligera no es compatible con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 ni con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows XP. [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] es compatible con la agrupación ligera.  
  
> [!NOTE]  
>  No se admite la ejecución de Common Language Runtime (CLR) con "agrupación ligera". Deshabilite una de las dos opciones: "clr enabled" o "agrupación ligera". Entre las características que dependen de CLR y que no funcionan correctamente en modo de fibra se encuentran el tipo de datos de jerarquía, la replicación y la administración basada en directivas.  
  
## <a name="see-also"></a>Consulte también  
 [clr enabled (opción de configuración del servidor)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled (opción de configuración del servidor)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)  
  
  
