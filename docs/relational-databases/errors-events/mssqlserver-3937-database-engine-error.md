---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4289b3e41de0e1652bd9cc033b2fab6ae8f42a60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043563"
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
