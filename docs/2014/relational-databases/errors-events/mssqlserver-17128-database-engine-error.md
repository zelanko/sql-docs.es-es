---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e3a2d500a16a90ce997273fad3eb7c2d8a82c1d6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553680"
---
# <a name="mssqlserver_17128"></a>MSSQLSERVER_17128
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|17128|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|INIT_NOBUFSPACE|  
|Texto del mensaje|initdata: memoria insuficiente para los búferes del kernel.|  
  
## <a name="explanation"></a>Explicación  
 Se ha producido un error en las reservas o las asignaciones de memoria iniciales del grupo de búferes, y SQL Server se cierra.  
  
## <a name="user-action"></a>Acción del usuario  
 Normalmente, se debe a que SQL Server se inicia en un equipo sumamente pequeño, mucho menor de lo que determinan los requisitos mínimos del sistema.  
  
  
