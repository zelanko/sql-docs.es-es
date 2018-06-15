---
title: disallow results from triggers (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4fa4fca7f98491a1a47069ff86c2ae2c7fbd70e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32863480"
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>disallow results from triggers (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice la opción **disallow results from triggers** para controlar si los desencadenadores devuelven conjuntos de resultados. Los desencadenadores que devuelven conjuntos de resultados pueden provocar un comportamiento inesperado en aplicaciones que no estén diseñadas para utilizarlos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Se recomienda establecer este valor en 1.  
  
 Si se asigna el valor 1, la opción **disallow results from triggers** se establece en el valor ON. El valor predeterminado para esta opción es 0 (OFF). Si a esta opción se le asigna el valor 1 (ON), se producirá un error cuando un desencadenador intente devolver un conjunto de resultados y el usuario recibirá el siguiente mensaje de error:  
  
 "Mensaje 524, nivel 16, estado 1, procedimiento \<nombre de procedimiento>, línea \<número de línea>  
  
 "Un desencadenador devolvió un conjunto de resultados pero la opción de servidor 'disallow_results_from_triggers' es true."  
  
 La opción **disallow results from triggers** se aplica a nivel de instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y determinará el comportamiento de todos los desencadenadores existentes de la instancia.  
  
 **disallow results from triggers** es una opción avanzada. Si va a usar el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo puede cambiar el valor No permitir resultados de desencadenadores si **Mostrar opciones avanzadas** está establecido en 1. La configuración surte efecto inmediatamente, sin necesidad de reiniciar un servidor.  
  
## <a name="see-also"></a>Ver también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
