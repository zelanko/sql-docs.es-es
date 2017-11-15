---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: a7d0100695085d94c645bb8dae21d10616f3145f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17128"></a>MSSQLSERVER_17128
  
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
  
