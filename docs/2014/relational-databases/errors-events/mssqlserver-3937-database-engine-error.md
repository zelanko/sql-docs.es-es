---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cac466e6eb50ad4b7a8848a1159963cb0fd35e22
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033299"
---
# <a name="mssqlserver_3937"></a>MSSQLSERVER_3937
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|MSSQLSERVER|  
|Id. de evento|3937|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|XACT_FILESTREAM_ROLLBACK_ERROR|  
|Texto del mensaje|Error al intentar notificar al controlador de filtro de secuencias de archivo que se revirtió una transacción. Código de error: 0x%0x.|  
  
## <a name="explanation"></a>Explicación  
 El controlador RsFx ha devuelto un error al emitir una notificación de reversión de una transacción. Este error suele provocarlo la escasez de recursos. Esto puede producir una pequeña pérdida de memoria en el controlador de filtro RsFx, pero ésta se liberará cuando se cierre el proceso sqlservr.exe que creó la transacción.  
  
## <a name="user-action"></a>Acción del usuario  
  
