---
title: in-doubt xact resolution (opción de configuración del servidor) | Microsoft Docs
description: Familiarícese con la opción "in-doubt xact resolution". Vea cómo determina el resultado predeterminado de las transacciones dudosas en SQL Server.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- distributed transactions [SQL Server], unresolved transactions
- unresolved transactions
- in-doubt xact resolution option
ms.assetid: 3426fd32-cad2-4f2f-8ca9-e0296cc12703
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 946f36bb379e5fde01f4232b01699405dd63aa8d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772418"
---
# <a name="in-doubt-xact-resolution-server-configuration-option"></a>in-doubt xact resolution (opción de configuración del servidor)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
## <a name="see-also"></a>Consulte también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
