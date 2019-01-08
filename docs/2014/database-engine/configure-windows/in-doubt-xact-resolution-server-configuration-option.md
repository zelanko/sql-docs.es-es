---
title: in-doubt xact resolution (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- distributed transactions [SQL Server], unresolved transactions
- unresolved transactions
- in-doubt xact resolution option
ms.assetid: 3426fd32-cad2-4f2f-8ca9-e0296cc12703
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 648f142eb80607412e13151098418c22e45f04bd
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640155"
---
# <a name="in-doubt-xact-resolution-server-configuration-option"></a>in-doubt xact resolution (opción de configuración del servidor)
  Use la opción **in-doubt xact resolution** para controlar el resultado predeterminado de las transacciones que el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) no consigue resolver. La incapacidad de resolver estas transacciones puede estar relacionada con un tiempo de inactividad de MS DTC o con un resultado de transacción inesperado en el momento de la recuperación.  
  
 La siguiente tabla enumera los valores de resultado posibles para resolver una transacción dudosa.  
  
|Valor del resultado|Descripción|  
|-------------------|-----------------|  
|0|Ninguna suposición. La recuperación no es correcta si MS DTC no puede resolver ninguna transacción dudosa.|  
|1|Suponer la confirmación. Se presupone que las transacciones MS DTC dudosas se han confirmado.|  
|2|Suponer anulación. Se presupone que las transacciones MS DTC dudosas se han anulado.|  
  
 Para minimizar la posibilidad de sufrir tiempos de inactividad prolongados, un administrador puede configurar esta opción para suponer una confirmación o una anulación, tal y como se muestra en el siguiente ejemplo.  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 2 -- presume abort  
GO  
RECONFIGURE  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 De forma alternativa, un administrador puede dejar el valor predeterminado (ninguna suposición) y permitir que la recuperación no sea correcta para dejar constancia del error del DTC, tal y como se muestra en el siguiente ejemplo.  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 1 -- presume commit  
GO  
reconfigure  
GO  
ALTER DATABASE pubs SET ONLINE -- run recovery again  
GO  
sp_configure 'in-doubt xact resolution', 0 -- back to no assumptions  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 **in-doubt xact resolution** es una opción avanzada. Si está usando el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo podrá cambiar el valor de **in-doubt xact resolution** si **show advanced options** se establece en 1. La configuración surte efecto inmediatamente, sin necesidad de reiniciar un servidor.  
  
> [!NOTE]  
>  La configuración coherente de esta opción en todas las instancias de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implicadas en cualquier transacción distribuida ayuda a evitar incoherencias en los datos.  
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
