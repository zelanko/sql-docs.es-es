---
title: MSSQLSERVER_17132 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 335ba6a544023fd4eec16cd7461e2e17c224020f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68131802"
---
# <a name="mssqlserver_17132"></a>MSSQLSERVER_17132
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|17132|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|INIT_NODESSPACE|  
|Texto del mensaje|Error al iniciar el servidor debido a una falta de memoria para el descriptor. Reduzca la carga de memoria no esencial o aumente la memoria del sistema.|  
  
## <a name="explanation"></a>Explicación  
No se pudo asignar suficiente memoria para almacenar el descriptor interno del servidor.  
  
## <a name="user-action"></a>Acción del usuario  
Agregue más memoria a la máquina. Puede ser útil seguir un procedimiento para solucionar problemas genéricos de memoria.  
  
