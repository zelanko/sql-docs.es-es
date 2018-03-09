---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: acd5e252c51787cd9d610d331fc545502a48db79
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|MSSQLSERVER|  
|Identificador del evento|3937|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|XACT_FILESTREAM_ROLLBACK_ERROR|  
|Texto del mensaje|Error al intentar notificar al controlador de filtro de secuencias de archivo que se revirtió una transacción. Código de error: 0x%0x.|  
  
## <a name="explanation"></a>Explicación  
El controlador RsFx ha devuelto un error al emitir una notificación de reversión de una transacción. Este error suele provocarlo la escasez de recursos. Esto puede producir una pequeña pérdida de memoria en el controlador de filtro RsFx, pero ésta se liberará cuando se cierre el proceso sqlservr.exe que creó la transacción.  
  
## <a name="user-action"></a>Acción del usuario  
