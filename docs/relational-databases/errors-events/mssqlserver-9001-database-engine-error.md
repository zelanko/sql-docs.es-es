---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 22767609a0281cc21a38d51716661ac98a8ffc24
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68118365"
---
# <a name="mssqlserver_9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|9001|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOG_NOT_AVAIL|  
|Texto del mensaje|El registro de la base de datos '%.*ls' no está disponible. Vea los mensajes de error relacionados en el registro de eventos. Corrija los errores y reinicie la base de datos.|  
  
## <a name="explanation"></a>Explicación  
El registro de la base de datos se dejó sin conexión. Normalmente esto indica un error grave que requiere reiniciar la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
Diagnostique otros errores y reinicie la sesión de SQL Server si aún no se ha reiniciado.  
  
