---
title: MSSQLSERVER_9003 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eb3fcdb8bc7921c8321cc25ec9380143e7f68a68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118347"
---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9003|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOG_INVALID_LSN|  
|Texto del mensaje|El número de examen del registro %S_LSN pasado al examen del registro de la base de datos '%.*ls' no es válido. This error may indicate data corruption or that the log file (.ldf) does not match the data file (.mdf). If this error occurred during replication, re-create the publication. De lo contrario, restaure la base de datos a partir de una copia de seguridad si el problema da lugar a un error durante el inicio.|  
  
## <a name="explanation"></a>Explicación  
Un componente pasó un número de flujo de registro no válido al administrador de registros para la base de datos. Podría corresponder a la replicación, a daños o a una incoherencia entre el archivo de datos principal y el registro.  
  
## <a name="user-action"></a>Acción del usuario  
Si esto ocurrió durante la replicación, vuelva a crear la publicación. De lo contrario, restaure una copia de seguridad.  
  
