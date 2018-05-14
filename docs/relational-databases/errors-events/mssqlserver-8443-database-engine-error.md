---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 75fb26c6ad2d49fe8a28a84cdecf8aa67564c6e8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8443|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SB_DIALOG_WO_CONV_GROUP|  
|Texto del mensaje|La conversación con id. '%.*ls' y el iniciador %d hace referencia a un grupo de conversaciones que falta ('%.\*ls'). Ejecute DBCC CHECKDB para analizar y reparar la base de datos.|  
  
## <a name="explanation"></a>Explicación  
La capa de metadatos devolvió NULL para el grupo de conversaciones. La base de datos ha resultado dañada de alguna manera. Un posible origen de los daños es un error de disco.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute DBCC CHECKDB en el modo de reparación para restaurar la base de datos a un estado coherente. Puede que se eliminen mensajes si es necesario para restablecer la coherencia. Investigue en los registros de errores del sistema para ver si la causa de este error es otro error del sistema.  
  
