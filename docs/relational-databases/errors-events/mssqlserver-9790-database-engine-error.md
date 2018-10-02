---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dd965940d43fdcc1e2420e8c5a43e512b45298e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840403"
---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9790|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|Texto del mensaje|No se puede enrutar el mensaje entrante. La base de datos del sistema MSDB que contiene la información de enrutamiento está en modo SINGLE USER.|  
  
## <a name="explanation"></a>Explicación  
Se produjo un error al intentar clasificar un mensaje recibido fuera de la conexión porque la base de datos MSDB estaba en modo SINGLE USER.  
  
## <a name="user-action"></a>Acción del usuario  
Cambie MSDB para que esté en modo MULTI USER con el comando ALTER DATABASE.  
  
