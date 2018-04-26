---
title: MSSQLSERVER_5515 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: b67a2eba3337da6f5ef81bb0a071371628f96cee
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver5515"></a>MSSQLSERVER_5515
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|MSSQLSERVER|  
|Identificador del evento|5515|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|FS_OPEN_CONTAINER_FAILED|  
|Texto del mensaje|No se puede abrir el directorio que contiene el archivo de FILESTREAM ''%.*ls''. El sistema operativo ha devuelto el código de estado de Windows 0x%x.|  
  
## <a name="explanation"></a>Explicación  
No se puede abrir el directorio especificado que contiene el archivo de FILESTREAM.  
  
## <a name="user-action"></a>Acción del usuario  
Para obtener información sobre la causa del error, vea el código de estado de Windows específico.  
  
