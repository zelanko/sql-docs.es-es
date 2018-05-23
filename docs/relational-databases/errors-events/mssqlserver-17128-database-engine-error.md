---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e21b6945d2eb18c32df8481e2a3e8170e642c82e
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver17128"></a>MSSQLSERVER_17128
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17128|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|INIT_NOBUFSPACE|  
|Texto del mensaje|initdata: memoria insuficiente para los búferes del kernel.|  
  
## <a name="explanation"></a>Explicación  
Se ha producido un error en las reservas o las asignaciones de memoria iniciales del grupo de búferes, y SQL Server se cierra.  
  
## <a name="user-action"></a>Acción del usuario  
Normalmente, se debe a que SQL Server se inicia en un equipo sumamente pequeño, mucho menor de lo que determinan los requisitos mínimos del sistema.  
  
