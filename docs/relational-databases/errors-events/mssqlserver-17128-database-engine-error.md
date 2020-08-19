---
description: MSSQLSERVER_17128
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1902d498a93555957b0c240d349a951327086382
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88410991"
---
# <a name="mssqlserver_17128"></a>MSSQLSERVER_17128
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
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
  
