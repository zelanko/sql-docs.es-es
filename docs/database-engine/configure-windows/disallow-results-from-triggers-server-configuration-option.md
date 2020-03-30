---
title: disallow results from triggers (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 28bf3b201d54798f26c9e887e86a9d0bed78ee15
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68011861"
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>disallow results from triggers (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice la opción **disallow results from triggers** para controlar si los desencadenadores devuelven conjuntos de resultados. Los desencadenadores que devuelven conjuntos de resultados pueden provocar un comportamiento inesperado en aplicaciones que no estén diseñadas para utilizarlos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Se recomienda establecer este valor en 1.  
  
 Si se asigna el valor 1, la opción **disallow results from triggers** se establece en el valor ON. El valor predeterminado para esta opción es 0 (OFF). Si a esta opción se le asigna el valor 1 (ON), se producirá un error cuando un desencadenador intente devolver un conjunto de resultados y el usuario recibirá el siguiente mensaje de error:  
  
 "Mensaje 524, nivel 16, estado 1, procedimiento \<nombre de procedimiento>, línea \<número de línea>  
  
 "Un desencadenador devolvió un conjunto de resultados pero la opción de servidor 'disallow_results_from_triggers' es true."  
  
 La opción **disallow results from triggers** se aplica en el nivel de instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y determina el comportamiento de todos los desencadenadores existentes en la instancia.  
  
 **disallow results from triggers** es una opción avanzada. Si va a usar el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo puede cambiar el valor No permitir resultados de desencadenadores si **Mostrar opciones avanzadas** está establecido en 1. La configuración surte efecto inmediatamente, sin necesidad de reiniciar un servidor.  
  
## <a name="see-also"></a>Consulte también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
