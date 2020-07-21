---
title: MSSQLSERVER_5235 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5235 (Database Engine error)
ms.assetid: 1aa7e6a5-7ccb-43c8-a1fd-d50e92e0a798
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b19e643a77a2cdd3d74d05f87480fe66e3b0cf60
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551260"
---
# <a name="mssqlserver_5235"></a>MSSQLSERVER_5235
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|5235|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC4_ERRORLOG_SUMMARY_PREMATURE_TERMINATION|  
|Texto del mensaje|[EMERGENCY] DBCC DBCC_COMMAND_DETAILS ejecutado por USER_NAME finalizó de forma anómala debido a un estado de error ERROR_STATE. Tiempo transcurrido: HOURS horas MINUTES minutos SECONDS segundos.|  
  
## <a name="explanation"></a>Explicación  
 Este es el mensaje de resumen que DBCC imprime en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se produce una finalización inesperada mientras se ejecuta el comando. El estado de error notificado en el mensaje define el tipo de finalización inesperada.  
  
 En la siguiente tabla se muestran y se definen los estados de error.  
  
|Estado de error|Definición|  
|-----------------|----------------|  
|State 0|La instrucción finalizó debido a un daño grave de los metadatos. Este mensaje irá acompañado de una o varias instancias de error 8930.|  
|State 1|La instrucción finalizó debido a un error interno de comprobación. Este mensaje irá acompañado de una o varias instancias de error 8967.|  
|State 2|Error en las comprobaciones básicas de las tablas del sistema del motor de almacenamiento principal. Este mensaje irá acompañado de una o varias instancias de error [7984](mssqlserver-7984-database-engine-error.md), 7985, [7986](mssqlserver-7986-database-engine-error.md), [7987](mssqlserver-7987-database-engine-error.md) o [7988](mssqlserver-7988-database-engine-error.md).|  
|State 3|Error en la reparación del modo de emergencia DBCC debido a que la base de datos no pudo iniciarse después de volver a generar el registro de transacciones. Este mensaje irá acompañado del error 7909.|  
|State 4|Se produjo un error de aserción o infracción de acceso durante la ejecución del comando.|  
|Estado 5|Se produjo un error desconocido que canceló inesperadamente el comando DBCC.|  
  
## <a name="user-action"></a>Acción del usuario  
 En la siguiente tabla se muestra la acción apropiada que debe llevar a cabo el usuario para el estado de error especificado.  
  
|Estado de error|Acción del usuario|  
|-----------------|-----------------|  
|State 0|Restaure mediante la copia de seguridad.|  
|State 1|Póngase en contacto con el Servicio de atención al cliente y soporte técnico (CSS) de [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|State 2|Restaure mediante la copia de seguridad.|  
|State 3|Restaure mediante la copia de seguridad.|  
|State 4|Póngase en contacto con el CSS.|  
|Estado 5|Vuelva a ejecutar el comando. Si el problema persiste, póngase en contacto con el CSS.|  
  
## <a name="see-also"></a>Consulte también  
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)  
  
  
