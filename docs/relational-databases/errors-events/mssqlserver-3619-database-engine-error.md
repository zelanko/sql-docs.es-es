---
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e38ff7b2f54048dc1408774df5e6b82837709b4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver3619"></a>MSSQLSERVER_3619
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3619|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SYS_NOLOG|  
|Texto del mensaje|No se pudo escribir un registro de punto de comprobación en la base de datos con id. %d. Espacio insuficiente para el registro. Póngase en contacto con el administrador de la base de datos para truncar el registro o asignar más espacio a los archivos de registro de base de datos.|  
  
## <a name="explanation"></a>Explicación  
El registro de transacciones se ha quedado sin espacio en disco.  
  
## <a name="user-action"></a>Acción del usuario  
Trunque el registro para liberar espacio o asigne más espacio al registro. Para obtener más información, vea "Solucionar problemas de un registro de transacciones lleno (Error 9002)" en los Libros en pantalla de SQL Server.  
  
